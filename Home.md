Welcome to libarchive!

## What is libarchive?

**Libarchive** is an open-source BSD-licensed C programming library
that provides streaming access to a variety of archive file formats.
The distribution also includes [[bsdtar|ManPageBsdtar1]] and [[bsdcpio|ManPageBsdcpio1]],
full-featured implementations of tar and cpio that use libarchive.

[[Many other programs|LibarchiveUsers]] use libarchive as well.

The libarchive library can work with a [[variety of different archive formats|LibarchiveFormats]], including [[tar|FormatTar]], [[cpio|FormatCpio]], [[pax|FormatPax]], [[Zip|FormatZip]], and [[ISO9660 images|FormatISO9660]].

When reading archives, libarchive uses a robust
automatic format detector that can automatically handle
archives that have been compressed with gzip, bzip2, xz,
lzip, and several other popular compression algorithms.

The libarchive library allows full flexibility over the
source and destination of the data:
There are convenience wrappers for reading
and writing archives to regular files on disk or to memory,
but you can register your own [[I/O functions|LibarchiveIO]]
to read and write archives to tape drives, network sockets,
or any other data source.

## How to Start

* [[Building Libarchive|BuildInstructions]]
* [[Programming Examples|Examples]]

## Where to get more information

* This Wiki (of course)
* libarchive-discuss@googlegroups.com mailing list
* [[Extensive manpages|ManualPages]] are included with the distribution.

## How to contribute

We [[welcome contributions|ContributingToLibarchiveInGithub]], of course.
If you need ideas, take a peek at the [[WishList]] and
the [[internals documentation|LibarchiveInternals]].

If you aren't able to help with C coding, we still appreciate
volunteers to help improve this Wiki documentation, answer
questions on the
[[mailing list|http://groups.google.com/group/libarchive-discuss]],
and help test libarchive as it continues to evolve.


