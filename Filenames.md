Libarchive's filename handling has evolved somewhat organically and at present there are some troubling inconsistencies that are causing headaches for some users.  The following is an attempt to enumerate the issues and ultimately propose an approach that libarchive *should* use going forward.

# The Problem

Naming files is a tricky business.  There are two fundamentally different approaches in common use and unfortunately, libarchive needs to be able to translate between them:

* POSIX identifies each file with a specific sequences of *bytes* terminated with a zero byte.  Typically, these bytes correspond to some sequence of characters, but that correspondence is not fixed; two users may name the same file using entirely different character sequences as long as they generate the same sequence of bytes.  Indeed, POSIX does not require the sequence of bytes identifying a file to have *any* meaningful interpretation in any character encoding at all.

* Newer systems, beginning with Windows NT (but now including Mac OS X and others) identify files with a specific sequence of *characters.*  These systems as a rule store the filenames on disk as some variant of Unicode, though they will translate various user character sets to and from Unicode as necessary.

This variation is reflected in archive formats as well:  old tar, cpio, and zip archives store filenames as a sequence of bytes; newer pax, zip, and ISO archives store filenames as a Unicode character sequence.  Of course, there are subtle variations that complicate this basic picture.

This is a challenge for libarchive because it needs to support both styles of archive with client software built around both sets of conventions:

* Software built around Unicode techniques expects to use Unicode filenames when reading and writing archives.  This is a problem when reading archives that store just byte sequences.  Generally, these archives do not specify any particular character encoding, so there is no robust basis for translating a byte sequence to or from Unicode.  The only information libarchive may have available is the "user character encoding", but there is no guarantee that this has any meaningful relation to the particular byte sequences used to identify a particular entry in a particular archive.

* Software built around POSIX conventions deals easily with old tar and cpio archives; such archives use sequences of bytes to identify files and software using POSIX conventions can simply transfer those sequences of bytes to library functions such as open() and fopen().   But libarchive also needs to allow such software to access archives that use character semantics for filenames.

Keep in mind that software using POSIX conventions does typically need to display filenames or allow users to enter them.  This implies that such software is using some (usually implicit) assumptions about the character encoding used by those filenames.

# Specific Cases That Need Consideration

To simplify the following discussion, I'll assume that software and archives using character semantics deal with UTF-8.  In practice, UTF-16 and UCS-4 are also common, but translating between either of those and UTF-8 is trivial.  I'll also ignore Unicode normalization issues for now.  I'll refer to software and archives that use byte-sequence conventions as "POSIX-convention", even though such conventions are common on non-POSIX systems as well.  So we have a number of cases we need to consider:

1. UTF-8 software working with UTF-8 archive formats.  Such software should be able to pass through UTF-8 filenames when reading or writing archives.

2. POSIX-convention software working with POSIX-convention archive formats.  Similarly, sequences of bytes should be able to pass through with no translation.

3. UTF-8 software *writing* POSIX-convention archives.  Filenames encoded in UTF-8 satisfy the requirements for POSIX-convention archives and can be written directly.  (Note that neither UTF-16 nor UCS-4 satisfy the requirements for POSIX-convention archives as they both permit zero bytes.)

4. UTF-8 software *reading* POSIX-convention archives.  This is a hard case.  Generally, archives do not specify a character encoding for filenames.  It is possible (and increasingly likely) that the filename happens to already be in UTF-8 but there is no way to know for sure.  It is also possible that the filename happens to be encoded in the same encoding as the local user's preference but again, there is no way that we can reliably detect this for sure.  (TODO:  The proposed long-term solution below currently punts this to the client software; clients must be able to handle both UTF-8 and arbitrary byte sequence filenames.  This is not ideal; there should be some way to simplify things for UTF-8 client software.)

5. POSIX-convention software *writing* UTF-8 archives.  Generally, POSIX-convention software does have some notion of the current user's preferred character set, so we should be able to reliably translate user-provided text into UTF-8.  (This assumes setlocale() has been called to set up the current character set information.)  However, the software may be relaying a filename obtained from elsewhere (for example, it may be copying entries from a POSIX-convention archive), so this is not entirely guaranteed.

6. POSIX-convention software *reading* UTF-8 archives.  In this case, we generally do have some notion of the current user's preferred character set and will usually be able to convert UTF-8 filenames to that character set.  (Of course, translating UTF-8 to an arbitrary character set will often fail.)  It is tempting to pass the UTF-8 filenames from the archive directly to the POSIX-convention software, but that would cause problems for software that expects the filenames to be in the current user's preferred character encoding.  Of course, libarchive may not be able to convert at all:  In the discussion for [Issue #587](https://github.com/libarchive/libarchive/issues/587), @wm4 challenged whether libarchive can ever safely assume that `setlocale()` has been called.  Without that, libarchive cannot know the user's preferred character set at all.  Certainly libarchive should never call `setlocale()`.

# Other Related issues

LHA stores a Windows code page with each filename.  This provides character semantics but does not force everything into Unicode.

Originally, Pax format could store short filenames using POSIX semantics (in the old ustar header) but long filenames had to be stored in UTF-8.  Since POSIX.2008, however, Pax format can store long filenames as "BINARY" as well.

# Solutions considered

I considered having a "utf8" and a "raw" pathname on each entry object.  In particular, that would allow storing both filenames for Zip and Pax archives that sometimes can have one of each.  However, this doesn't support LHA and there's not really a compelling reason to keep both available.

# Proposed Long-term Solution

Libarchive's API distinguishes two different areas of filename handling:  filenames are stored on entry objects, and the format handlers copy data between entry object fields and archive entries.  The following discussion treats these separately:

## Entry objects

If we store pathnames together with the character set, we can cover all of the cases above:
  * Set the character set to "UTF8" to mark a UTF-8 filename
  * Set the character set to NULL to mark a raw (POSIX-semantic) filename
  * Store some other character set for LHA

This allows us to defer character set conversions as late as possible in the common cases, which reduces the possibility of surprises.

## Reading archives

When **reading** archives, the filename from the archive will be stored in the entry in the archive format.  If the character set is known, it will be stored as well.  If it is not known, the character set will be NULL.  This requires no character-set conversion within libarchive.

Exception:  Other Unicode formats should be converted to UTF-8, to make it simpler for client software to support multiple archive formats.  This is lossless and should be safe in all cases.

TODO:  In particular, UTF-8 client software may be faced with raw POSIX-convention filenames that it can do nothing with.

TODO:  Even worse:  Common behavior on POSIX systems demands that UTF-8 filenames be translated (via iconv or similar) to the user's local preferred character set.  This proposal pushes that common requirement onto the client, which is awkward.

## Writing archives

When **writing** archives, the filename in the entry object will be used directly if possible:

In particular, if the filename is UTF-8 and the archive supports UTF-8 filenames, it will be stored as-is.

If the filename character set is unknown, then it will be stored raw.

If the filename character set is known and we have iconv, then we can try to convert it to UTF-8 if the archive supports that.  If we don't have iconv, we would have to store it raw.

## Special cases

Joliet requires a Unicode filename; it has no option for raw filenames.  This leaves a few options:

 * If the character set is UTF-8, then we can use it directly.

 * If the character set is known, we can use iconv() to convert to Unicode

 * If the character set is not known but the bytes of the filename are consistent with UTF-8, the filename can be treated as UTF-8

 * Otherwise, the format will use iconv() to attempt to convert the filename from the current user's default character encoding to UTF-8.  If this succeeds, the converted filename will be used.  Note:  This step will necessarily fail if iconv() is unavailable or setlocale() has not been called.

 * As a fallback, we will assume the filename is in ISO-8859-1 and converted to UTF-8 accordingly.  (Note this does not require iconv() or any similar software package.  Converting ISO-8859-1 to UTF-8 is trivial:  byte values less than 128 are preserved as-is, byte values 128-255 are converted to two-byte UTF-8 equivalents.)

ISO9660 only supports US-ASCII.

Note that bsdtar on many POSIX systems will never create an archive containing a UTF-8 filename.  (Unless it went to some effort to identify whether the user had a UTF-8 locale setting.)  This may surprise some people.  (On Windows, the directory-traversal logic should probably provide UTF-8 filenames.)

# Proposed Interim Solution

Libarchive avoids backward-incompatible API or ABI changes within a major version, so we will need to take some additional steps in libarchive 3 to preserve compatibility with the full changes above being implemented in libarchive 4.

* The current "_w" methods will disappear in libarchive 4.  TODO: How should they behave now?

* TODO: `archive_entry_pathname` above behaves differently than today.  How do we resolve that?

* TODO:  How should other methods behave now?  In libarchive 4?

* TODO:  What about user name, group name?

* TODO:  I've long wanted to add a "Comment" field to the archive entry object.  Can we assert UTF-8 for that?