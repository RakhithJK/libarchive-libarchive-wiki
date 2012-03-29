# About the Cpio format

AT&T used Unix fairly extensively in the 1970s and developed a special in-house version that included a variety of new tools.
Among these tools were the "find" and "cpio" utilities designed by Dick Haight.
These were designed to work together:
the "find" utility could list filenames; the "cpio" utility read filenames and then copied those files to another directory or into a "cpio archive."
The "cpio" utility was first released outside of AT&T as part of the Programmer's Work Bench (PWB/UNIX 1.0) in 1977.

The cpio program and file format were standardized in 1985 by POSIX.
For many years, debate raged over whether tar and cpio could reasonably both be included by the same standard.
This was resolved in 2001:
Both utilities were dropped from the standard and were replaced by the new "pax" utility that could read and write both archive formats.
Over the years, there have been a number of variant cpio formats, mostly driven by system vendors such as HP and Sun.

Detailed descriptions of cpio formats and details of libarchive's implementation
can be found on the following pages:

* [[The cpio.5 man page|ManPageCpio5]] provides technical details of several cpio formats and extensions.
* The [[POSIX standard for pax|http://pubs.opengroup.org/onlinepubs/9699919799/utilities/pax.html]] includes the official definitions for the "portable octet-oriented cpio format", widely known as "odc" or "old character" format.
