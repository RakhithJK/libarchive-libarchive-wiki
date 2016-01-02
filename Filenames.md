Libarchive's filename handling has evolved somewhat organically and at present there are some troubling inconsistencies that are causing headaches for some users.  The following is an attempt to enumerate the issues and ultimately propose an approach that libarchive *should* use going forward.

# The Problem

Naming files is a tricky business.  There are two fundamentally different approaches in common use and unfortunately, libarchive needs to be able to translate between them:

* POSIX identifies files with a specific sequences of *bytes* terminated with a zero byte.  Typically, these bytes correspond to some sequence of characters, but that correspondence is not fixed; two users may name the same file using entirely different character sequences as long as they generate the same sequence of bytes.  Indeed, POSIX does not require the sequence of bytes identifying a file to have *any* meaningful interpretation in any character encoding at all.

* Newer systems, beginning with Windows NT (but now including Mac OS X and others) identify files with a specific sequence of *characters.*  These systems as a rule store the filenames on disk as some variant of Unicode, though they will translate various user characters sets to and from Unicode as necessary.

This variation is reflected in archive formats as well:  old tar, cpio, and zip archives store filenames as a sequence of bytes; newer pax, zip, and ISO archives store filenames as a Unicode character sequence.  (Just to make things even more interesting: old cpio and zip archives technically allow zero bytes within filenames.)

This is a challenge for libarchive because it needs to support both styles of archive with software built around both sets of conventions:

* Software built around Unicode techniques expects to use Unicode filenames when reading and writing archives.  This is a problem when reading archives that store just byte sequences.  Generally, these archives do not specify any particular character encoding, so there is no robust basis for translating to or from another character set.  The only information libarchive may have available is the "user character encoding", but there is no guarantee that this has any meaningful relation to the particular byte sequences used to identify a particular file in a particular archive.

* Software built around POSIX conventions deals easily with old tar and cpio archives; such archives use sequences of bytes to identify files and software using POSIX conventions can simply transfer those sequences of bytes to library functions such as open() and fopen().   But libarchive also needs to allow such software to access archives that use character semantics for filenames.

Keep in mind that software using POSIX conventions does typically need to display filenames or allow users to enter them.  This implies that such software is using some (usually implicit) assumptions about the character encoding used by those filenames.

# Specific Cases That Need Consideration

To simplify the following discussion, I'll assume that software and archives using character semantics deal with UTF-8.  In practice, UTF-16 and UCS-4 are also relatively common, but translating between either of those and UTF-8 is trivial.  I'll also ignore Unicode normalization issues for now.  I'll also refer to software and archives that use byte-sequence conventions as "POSIX-convention", even though such conventions are common on non-POSIX systems as well.  So we have a number of cases we need to consider:

1. UTF-8 software working with UTF-8 archive formats.  Such software should be able to pass through UTF-8 filenames when reading or writing archives.

2. POSIX-convention software working with POSIX-convention archive formats.  Similarly, sequences of bytes should be able to pass through with no translation.

3. UTF-8 software writing POSIX-convention archives.  Filenames encoded in UTF-8 satisfy the requirements for POSIX-convention archives and can be written directly.  (Note that neither UTF-16 nor UCS-4 satisfy the requirements for POSIX-convention archives as they both permit zero bytes.)

4. UTF-8 software reading POSIX-convention archives.  This is a hard case.  Generally, archives do not specify a character encoding for filenames.  It is possible (and increasingly likely) that the filename happens to already be in UTF-8 but there is no way to know for sure.  It is also possible that the filename happens to be encoded in the same encoding as the local user's preference but again, there is no way that we can reliably detect this for sure.

5. POSIX-convention software writing UTF-8 archives.  Generally, POSIX-convention software does have some notion of the current user's preferred character set, so we should be able to reliably translate user-provided text into UTF-8.  However, the software may be relaying a filename obtained from elsewhere (for example, it may be copying entries from a POSIX-convention archive), so this is not entirely guaranteed.

6. POSIX-convention software reading UTF-8 archives.  In this case, we generally do have some notion of the current user's preferred character set and will usually be able to convert UTF-8 filenames to that character set.  (Of course, translating UTF-8 to an arbitrary character set will often fail.)  It is tempting to pass the UTF-8 filenames from the archive directly to the POSIX-convention software, but that would cause problems for software that expects the filenames to be in the current user's preferred character encoding.

# Proposed Long-term Solution

Practically speaking, all extant archive formats support either UTF-8 filenames, POSIX-convention byte sequence filenames, or both.  (The only exceptions I know of are the ISO formats:  ISO9660 specifies uppercase US-ASCII filenames and Joliet specifies UTF-16 filenames.  Rockridge extends ISO9660 to support POSIX-convention byte sequence filenames.)

Libarchive's API distinguishes two different areas of filename handling:  filenames are stored on entry objects, and the format handlers copy data between entry object fields and archive entries.  The following discussion treats these separately:

## Entry objects

Libarchive's entry object should provide methods that pass through the available filename information unchanged:

* `archive_entry_pathname_utf8` returns the UTF-8 filename if available or NIL if no such filename was provided by the archive.  Similarly, `archive_entry_set_pathname_utf8` sets a UTF-8 filename on the entry object.

* `archive_entry_pathname_raw` returns the POSIX-convention byte sequence filename if one was available.  Note that this may happen to be in UTF-8 but there is no guarantee.  Similarly, `archive_entry_set_pathname_raw` sets a raw filename on the entry object.

Note that the two separate filename methods above are completely independent; any particular entry object may have either, both, or neither of these values set.  Also note that no character-set conversion is done by these methods.

TODO:  Most software, of course, does not want to deal with the ambiguity above, so libarchive should provide convenience methods with well-defined behavior...

## Reading archives

When **reading** archives, these filenames will be set from the data in the archive as follows:

* If the archive entry contains a UTF-8 filename, the UTF-8 filename will be set.

* If the archive entry contains a POSIX-convention filename, the raw filename will be set.

Note that it is possible for both filenames to be set to different values:  Pax, Zip, ISO9660, and other formats can and will store multiple filenames on the same entry.  Also note that no character set conversion is done at the point where the archive is being read.  (Exception:  formats that store other Unicode encodings will be converted to UTF-8.)

## Writing archives

When **writing** archives, the data in the entry object will be used as follows:

* If both raw and UTF-8 filenames are present, the raw filename will be ignored.  In particular, naively copying an entry from an archive that stores both filenames to another archive of the same format may change the raw filename to a copy of the UTF-8 filename.  This may be surprising, but is consistent with the intent of the various standards that the two filenames be substantially the same.

* When writing POSIX-convention filenames in archives, a raw filename from the entry will be copied as-is if it is present, otherwise a UTF-8 filename will be stored as a zero-terminated sequence of bytes.

* When writing Unicode filenames in archives, a UTF-8 filename can be used directly.  In some cases, filenames will need to be translated from UTF-8 to UTF-16 or UCS-4.  In other cases, the Unicode filename may need to be normalized, depending on the archive format requirements.  Any such normalization is done by the format handler at the point where the archive is being written.

* If the only filename available is a raw filename and the archive supports raw and Unicode filenames, the format should write only the raw part of the entry.

* If the only filename available is a raw filename and the archive requires a Unicode filename, the format logic will attempt to convert the raw filename to Unicode using the logic below.  Note that this occurs at the point where the archive entry is being written.  (TODO: Should the format write the resulting UTF-8 back to the entry for reference?)

 * If the bytes of the filename are consistent with UTF-8, the filename will be treated as UTF-8.

 * Otherwise, the format will use iconv() to attempt to convert the filename from the current user's default character encoding to UTF-8.  If this succeeds, the converted filename will be used.  Note:  On systems where iconv is unavailable, this step will be skipped.

 * As a fallback, we will assume the filename is in ISO-8859-1 and converted to UTF-8 accordingly.  (Note this does not require iconv() or any similar software package.  Converting ISO-8859-1 to UTF-8 is trivial:  byte values less than 128 are preserved as-is, byte values 128-255 are converted to two-byte UTF-8 equivalents.)

## Special cases

* ISO9660 uses US-ASCII which is a strict subset of UTF-8.  On reading, we can just store the US-ASCII filename as the UTF-8 name in the entry object.  On writing, ...


# Proposed Interim Solution

The long-term solution may not be immediately implementable.  Libarchive avoids backward-incompatible API or ABI changes within a major version, so we may need to make limited changes in libarchive 3 to retain backwards compatibility with more extensive changes being deferred to libarchive 4.

TODO