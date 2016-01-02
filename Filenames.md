Libarchive's filename handling has evolved somewhat organically and at present there are some troubling inconsistencies that are causing headaches for some users.  The following is an attempt to enumerate the issues and ultimately propose an approach that libarchive *should* use going forward.

# The Problem

Naming files is a tricky business.  There are two fundamentally different approaches in common use and unfortunately, libarchive needs to be able to translate between them:

* POSIX identifies files with a specific sequences of *bytes* terminated with a zero byte.  Typically, these bytes correspond to some sequence of characters, but that correspondence is not fixed; two users may name the same file using entirely different character sequences as long as they generate the same sequence of bytes.  Indeed, POSIX does not require the sequence of bytes identifying a file to have *any* meaningful interpretation in any character encoding at all.

* Newer systems, beginning with Windows NT (but now including Mac OS X and others) identify files as a specific sequence of *characters.*  These systems as a rule store the filenames on disk as some variant of Unicode, though they will translate various user characters sets to and from Unicode as necessary.

This variation is reflected in archive formats as well:  old tar, cpio, and zip archives store filenames as a sequence of bytes; newer pax, zip, and ISO archives store filenames as a Unicode character sequence.  (Just to make things even more interesting: old cpio and zip archives technically allow zero bytes within filenames.)

This is a challenge for libarchive because it needs to support both styles of archive with software built around both sets of conventions:

* Software built around POSIX conventions deals easily with old tar and cpio archives; such archives use sequences of bytes to identify files and software using POSIX conventions can simply transfer those sequences of bytes to library functions such as open() and fopen().   But libarchive also needs to allow such software to access archives that use character semantics for filenames.

* Software built around Unicode techniques expects to use Unicode filenames when reading and writing archives.  This is a problem when reading archives that store just byte sequences.  Generally, these archives do not specify any particular character encoding, so there is no basis for translating to or from another character set.  The only information libarchive may have available is the "user character encoding", but there is no guarantee that this has any meaningful relation to the particular byte sequences used to identify a particular file in a particular archive.

# Specific Cases That Need Consideration

To simplify the following discussion, I'll assume that software and archives using character semantics deal with UTF-8.  In practice, UTF-16 and UCS-4 are also relatively common, but translating between either of those and UTF-8 is trivial.  I'll also ignore Unicode normalization issues for now.  I'll also refer to software and archives that use byte-sequence conventions as "POSIX-convention", even though such conventions are common on non-POSIX systems as well.  So we have a number of cases we need to consider:

1. UTF-8 software working with UTF-8 archive formats.  Such software should be able to pass through UTF-8 filenames when reading or writing archives.

2. POSIX-convention software working with POSIX-convention archive formats.  Similarly, sequences of bytes should be able to pass through with no translation.

3. UTF-8 software writing POSIX-convention archives.  Filenames encoded in UTF-8 satisfy the requirements for POSIX-convention archives and can be written directly.

4. UTF-8 software reading POSIX-convention archives.  This is a hard case.  Generally, archives do not specify a character encoding for filenames.  It is possible (and increasingly likely) that the filename happens to already be in UTF-8 but there is no way to know for sure.  It is also possible that the filename happens to be encoded in the same encoding as the local user's preference but again, there is no way that we can reliably detect this for sure.

5. POSIX-convention software writing UTF-8 archives.  Generally, POSIX-convention software does have some notion of the current user's preferred character set, so we should be able to reliably translate user-provided text into UTF-8.  However, the software may be relaying a filename obtained from elsewhere (for example, it may be copying entries from a POSIX-convention archive), so this is not guaranteed.

6. POSIX-convention software reading UTF-8 archives.  In this case, we generally do have some notion of the current user's preferred character set and should be able to reliably convert UTF-8 filenames to that character set.

# Proposed Long-term Solution

TODO

# Proposed Interim Solution

The long-term solution may not be immediately implementable.  Libarchive avoids backward-incompatible API or ABI changes within a major version, so we may need to make limited changes in libarchive 3 to retain backwards compatibility with more extensive changes being deferred to libarchive 4.
