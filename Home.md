Welcome to libarchive!

## What is libarchive?

**Libarchive** is an open-source BSD-licensed C programming library
that provides streaming access to a variety of archive file formats.
The distribution also includes [[bsdtar|ManPageBsdtar1]] and [[bsdcpio|ManPageBsdcpio1]],
full-featured implementations of tar and cpio that use libarchive.

[[Many other programs|LibarchiveUsers]] use libarchive as well.

The libarchive library can work with a [[variety of different archive formats|LibarchiveFormats]], including tar, cpio, pax, [[Zip|FormatZip]], and [[ISO9660 images|FormatISO9660]].

When reading archives, libarchive uses a robust
automatic format detector that can automatically handle
archives that have been compressed with gzip, bzip2, xz,
lzip, and several other popular compression algorithms.

The libarchive library allows full flexibility over the
source and destination of the data:
You can read a gzip-compressed tar archive from a socket
and extract the files to buffers in memory.
Similarly, you can synthesize data in memory and use it
to generate an ISO9660 image that you write out to a pipe.
There are convenience wrappers, of course, for reading
and writing archives to regular files on disk.

## Where to get more information

* This Wiki (of course)
* libarchive-discuss@googlegroups.com mailing list
* [[Extensive manpages|ManualPages]] are included with the distribution.

## How to contribute

