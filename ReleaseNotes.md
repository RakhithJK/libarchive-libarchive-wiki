Release notes for past and future libarchive versions.

Also see [[WishList]] for new feature ideas that would be nice to see
someday but aren't in the following schedule.
Since libarchive depends entirely on volunteer labor, the scheduling
and features for future releases are pure guesswork.
The reality will depend on who is interested enough to actually do
the work.

Alpha and Beta releases are not listed here.
They are not recommended for general use, though we usually leave them available in the Downloads section for historical reference.

## Libarchive 3.4.0
_Released: Jun 11, 2019_

### New features
* Support for file and directory symlinks on Windows
* Read support for RAR 5.0 archives
* Read support for ZIPX archives with xz, lzma, ppmd8 and bzip2 compression
* Support for non-recursive list and extract
* New tar option: --exclude-vcs
* Improved file attribute support on Linux and file flags support on FreeBSD
* 64-bit ar format support

### Important bugfixes
* fix reading Android APK archives ([#1055](https://github.com/libarchive/libarchive/issues/1055))
* fix problems related to unreadable directories ([#1167](https://github.com/libarchive/libarchive/issues/1167))
* patches from OpenBSD to libarchive_fe/passphrase.c
* support extracting ACLs with in-entry comments ([#1096](https://github.com/libarchive/libarchive/issues/1096))
* support extracting extattrs as non-root on non-user-writable files ([#1023](https://github.com/libarchive/libarchive/issues/1023))
* a two-digit number of OSS-Fuzz issues was resolved in this release
* various resource leak, use-after-free and crash fixes

## Libarchive 3.3.3
_Released: Sep 03, 2018_

### New features
* support for zstandard read and write filters

### Important bugfixes
* NO_OVERWRITE doesn't change existing directory attributes
* Many fixes for building with Visual Studio
* Avoid super-linear slowdown on malformed mtree files

## Libarchive 3.3.2
_Released: Jul 09, 2017_

* NFSv4 ACL support for Linux (librichacl)

## Libarchive 3.3.1
_Released: Feb 26, 2017_

### New features
* Tar format can archive and restore NFSv4 ACLs on FreeBSD, Linux, and macOS. This is fully interoperable with star.
* Tar format can read and write SCHILY.xattr extended file attributes in addition to the LIBARCHIVE.xattr format, thanks to Stefan Berger. This provides compatibility with archives created by star and GNU tar.
* Many bugs reported by the OSS-Fuzz project have been fixed.
* Ngie Cooper fixed a number of issues reported by the Coverity source scanner.
* Jan Osusky contributed improvements to libarchive's file detection logic.

## Libarchive 3.2.2
_Released: Oct 24, 2016_

### Security Fixes
* Four security bugs discovered by the FreeBSD project ([#743](https://github.com/libarchive/libarchive/issues/743))

## Libarchive 3.2.1
_Released: Jun 20, 2016_

## Libarchive 3.2.0
_Released: Apr 30, 2016_

### New features
* bsdcat: New command-line program automatically detects and decompresses a variety of files
* LZ4 compression
* Warc format support
* 'Raw' format writer
* Zip: Support archives >4GB, entries >4GB
* Zip: Support encrypting and decrypting entries
* Zip: Support experimental streaming extension
* Identify encrypted entries in several formats
* Libarchive now builds on AIX
* Libarchive now builds for Android
* New --clear-nochange-flags option to bsdtar tries to remove noschg and similar flags before deleting files
* New --ignore-zeros option to bsdtar to handle concatenated tar archives
* Use multi-threaded LZMA decompression if liblzma supports it
* Expose version info for libraries used by libarchive

### Notable Bug Fixes
* Many crash bugs fixed
* Many test bugs fixed
* Fixes to several formats to correctly handle empty filenames
* Limit recursion when selecting decompression; don't crash on quines
* Improved handling of sparse files, including files that consist of only a single large hole
* Improved test for extraction through symlinks
* Remove some properties from "restricted pax" that prevent using libarchive to build bit-for-bit identical results.
* Reduce memory usage when reading corrupted RAR archives
* Warn if hardlink extraction fails due to a missing target
* Limit recursion when assembling directories from ISO images

### Security fixes
CVE-2016-1541, aka TALOS-CAN-155:  Libarchive 3.1.2 and early mishandle the "compressed" and "uncompressed" sizes in certain Zip archive entries in a way that would allow someone to overwrite parts of the heap in a controlled fashion. 

## Libarchive 3.1.2
_Released: Feb 9, 2013_

## Libarchive 3.1.1
_Released: Jan 13, 2013_

## Libarchive 3.1.0
_Released: Jan 13, 2013_

### New features
* Added support for lrzip
* Added support for lzop
* Added support for grzip compression
* Added filters for base64 and uuencode
* Added support for writing tar v7 format
* Added support for resource-forks in Zip archives
* Added funtions to manually set filters and formats

## Libarchive 3.0.3
_Released: Jan 12, 2012_

* A fairly serious bug (described in [http://code.google.com/p/libarchive/issues/detail?id=222 Issue 222]) that caused crashes when archiving sparse files is fixed.
* There are also a number of other portability and build fixes.

## Libarchive 3.0.2
_Released: Dec 24, 2011_

### Backwards-incompatible API changes:
* The public interfaces consistently use int64_t instead of off_t, ino_t, uid_t, gid_t, and dev_t.
* New iconv integration provides deep support for converting filenames between different character sets.  It also fixes some long-standing problems with libarchive's handling of Unicode filenames in Pax, Zip, ISO, and other formats.
* Some old libarchive 1.x APIs have been removed.
* Some libarchive 2.x APIs have been deprecated; they'll continue to be supported until libarchive users have had plenty of time to migrate to the newer interfaces.  (In particular, function names have changed to prefer "free" to "finish", "filter" to "compression", and a few other small adjustments.)

### New features:
* New readers: RAR, LHA/LZH, CAB reader, 7-Zip
* New writers: ISO9660, XAR
* Improvements to many formats, especially including ISO9660 and Zip, 
* Stackable write filters allow you to write, e.g., tar.gz.uu in a single pass.
* Exploit seekable input - New "seekable" Zip reader can exploit the Zip Central Directory when it's available; the old "streamable" Zip reader is still fully supported for cases where seeking is not possible.
* Mac OS extended attribute support.  Thanks to Apple for releasing their patches.
* Many, many bug fixes.  More than 100 bugs have been marked "Fixed" in the Issue Tracker.

## Libarchive 2.8.5
_Released September 3, 2011_

## Libarchive 2.8.4
_Released June, 2010_

## Libarchive 2.8.3
_Released March, 2010_

## Libarchive 2.8.2
_Released March, 14, 2010_

* Fix NULL deference for short self-extracting zip archives.
* Don't dereference symlinks on Linux when reading ACLs.
* Better detction of SHA2 support for old OpenSSL versions.
* Fix parsing of input files for bsdtar -T.
* Do not leak setup_xattr into the global namespace.

## Libarchive 2.8.1
_Released March, 6, 2010_

* Fix build when an older libarchive is already installed
* Use O_BINARY opening files in bsdtar
* Include missing archive_crc32.h
* Correctly include iconv.h required by libxml2.

## Libarchive 2.8.0
_Released February 5, 2010_

* xar reader, uudecode support, and rpm support by Michihiro NAKAJIMA
* Fixes for MinGW and other Windows environments - libarchive now builds and runs cleanly with MinGW, Visual Studio, Cygwin, and other Windows development environments.
* Other portability improvements.  Brad King and others at Kitware have helped to set up a CDash test dashboard which should help us maintain a very high degree of portability moving forward.  They've also helped iron out a number of problems with the CMake build support in the libarchive distribution.
* zisofs reading and other ISO9660 improvements by Michihiro NAKAJIMA
* Zip writer - Anselm Strauss implemented most of this for Google Summer of Code 2008.  Joerg Sonnenberger worked out the remaining issues.

### Known issues:
* Build failures on FreeBSD 6 (OpenSSL issue), Windows/Borland C
* Miscellaneous test failures on MacOS
* Long filenames (over 260 characters) not supported by bsdtar on Windows
* Extended Attribute support triggers a bug in some versions of FreeBSD running ZFS

## Libarchive 2.7.1
_Released August 4, 2009_

* Issue 30: Fix reading xz-compressed archives that require large decompression buffers
* Issue 24: Fix hang reading truncated ISO archives.
* Issue 25: Fix reading body of first regular file in mtree archive.
* Issue 21: Work around timezone-related test failure (better fix will be in 2.8)
* Fix failure to read gzip files signed with gzsig (and other gzip files with "extra data")

## Libarchive 2.7.0
_Released April 17, 2009_

* Much improved Windows support, thanks largely to Michihiro NAKAJIMA.  In particular, the test suites now build and run on Windows.
* Support for building with "cmake" on a wide variety of platforms, thanks to Christian Ehrlicher and Michihiro.
* Support for concatenated gzip streams.
* Stackable read filter support.
* Eliminated Yacc/Bison requirement for building by rewriting date parser in plain C.
* Complete extended attribute support for FreeBSD, fixed extended attribute support for Linux
* Improved support for AIX, Tru64, and GNU Hurd, thanks to Björn Jacke
* Flexible options framework by Michihiro NAKAJIMA
* Support for reading and writing XZ format, thanks to Per Øyvind Karlsen and Michihiro.
* Support for reading Joliet extensions, thanks to Andreas Henriksson
* Support for mtree hash and CRC options, thanks to Michihiro NAKAJIMA
* Improved support for Cygwin, thanks to Charles Wilson

### Known Issues
* Building under MinGW is badly broken.  We plan to fix this for 2.8.
* A couple of libarchive tests fail when built with Visual Studio because of error-handling differences between Windows and Posix system libraries.

## Libarchive 2.6.2
_Released February, 2009_

* Fixed minor build issues on Linux and Solaris
* Fixed bsdtar adding null bytes to shar archive output
* Fixed crash when clients don't register skip callback

## Libarchive 2.6.1
_Released January, 2009_

* Fixed Issue 1: archive.h doesn't export required definitions
* Fixed Issue 3: Some empty entries in .zip files not extracted correctly
* Fixed multiple substitutions in bsdtar -s
* Fix an occasional failure extracting gzip-compressed archives
* Fix minor build problems on Cygwin and a few other platforms

## Libarchive 2.6
_Released December, 2008_

* LZMA read support, thanks to Miklos Vajna
* Windows build improvements, thanks to Ivailo Petrov, Kees Zeelenberg, and Vishant Singh
* New command-line parser provides uniform long-option support on all platforms
* Birthtime support, thanks to Pedro Giffuni
* archive_entry now tracks which values have been set.  In particular, this fixes a problem with extracting from zip archives that don't provide the file size in advance.  The restore-to-disk code now enforces file sizes only if a file size was specified.
* Many small improvements to UTF8 and unicode handling.
* mtree and shar performance improvements, thanks to Joerg Sonnenberger

## Libarchive 2.5
_Released July 2, 2008_

## Libarchive 2.4
_Released October, 2007_

## Libarchive 2.3
_Released September, 2007_

## Libarchive 2.2
_Released May, 2007_

## Libarchive 2.1
_Released April, 2007_

## Libarchive 2.0
_Released March, 2007_

Libarchive 2.0 fixed a couple of early API gaffes but mostly it introduced a regression suite that has helped immensely to improve stability.
It also introduced some [significant performance improvements](http://lists.freebsd.org/pipermail/freebsd-current/2007-March/069860.html).

## Libarchive 1.x

A "portable" release of libarchive and associated tools was first released in early 2006.

## Early Libarchive

Development of libarchive first began in 2003.
The FreeBSD project was generous enough to incubate the project; the library was first officially released as part of FreeBSD 5.3 in November 2004 and bsdtar was added as an option shortly thereafter.
Bsdtar became the default system tar in FreeBSD 6.0, released in November 2005.