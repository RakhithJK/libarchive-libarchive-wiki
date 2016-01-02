**Unfinished attempt to sort out how libarchive should handle filenames.**

Naming files is a tricky business.  There are two fundamentally different approaches in common use and unfortunately, libarchive needs to be able to translate between them:

* POSIX identifies files with a specific sequences of *bytes* terminated with a zero byte.  Typically, these bytes correspond to some sequence of characters, but that correspondence is not fixed; two users may name the same file using entirely different character sequences as long as they generate the same sequence of bytes.  Indeed, POSIX does not require the the sequence of bytes identifying a file has *any* meaningful interpretation in any character encoding at all.

* Newer systems, beginning with Windows NT (but now including Mac OS X and others) identify files as a specific sequence of *characters.*  These systems as a rule store the filenames on disk as some variant of Unicode, though they will translate various user characters sets to and from Unicode as necessary.

This variation is reflected in archive formats as well:  old tar, cpio, and zip archives store filenames as a sequence of bytes; newer pax, zip, and ISO archives store filenames as a Unicode character sequence.

This is a challenge for libarchive because it needs to support both styles of archive with software built around both sets of conventions:

* Software built around POSIX conventions deals easily with old tar and cpio archives; such archives use sequences of bytes to identify files and software using POSIX conventions can simply transfer those sequences of bytes to library functions such as open() and fopen().   But libarchive also needs to allow such software to access archives that use character semantics for filenames.

* Software built around Unicode techniques expects to use Unicode filenames when reading and writing archives.  This is a problem when reading archives that store just byte sequences.  Generally, these archives do not specify any particular character encoding, so there is no basis for translating to or from another character set.  The only information libarchive may have available is the "user character encoding", but there is no guarantee that this has any meaningful relation to the particular byte sequences used to identify a particular file in a particular archive.

