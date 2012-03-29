# About the Tar format

First Edition UNIX included a tape backup program called "tap".
Since it was designed around the capabilities of the First Edition filesystem,
it did not have a concept of "group" (First Edition only had "user" and "other" permission bits) and used a 16-bit time format.
Fourth Edition UNIX extended the file system capabilities and replaced "tap" with a new "tp" program for creating and reading tape backups.
Similarly, when Seventh Edition UNIX was released in January 1979, it featured a new set of file system features and a new tape backup program called "tar" (for "Tape ARchiver").

Until 1985, the "tar format" was just the format supported by the "tar program."
Of course, there were several other implementations by this point and compatibility was starting to be a concern.
So the first POSIX standard included a specification for "UNIX Standard TAR" format (ustar) that extended the original tar format slightly.
In particular, it included user and group names (previously, tar archives had only included user and group numbers), supported pathnames up to 255 characters (instead of the 100 of the earlier version), and defined a signature value that could be used to identify compliant archives.

One of the more influential implementations was John Gilmore's pdtar program which appeared around the same time as the first POSIX standard.
In particular, pdtar formed the basis of GNU tar, which extended the pdtar format (which was not the same as ustar) many times over the years, adding a number of new features that were missing from ustar.
Other tar implementations also extended ustar in various ways, but none of
these were as influential as GNU tar.

In 2001, POSIX dropped the "tar" program from the standard.
POSIX had been trying for some time to reconcile the differences between the tar and cpio
programs and finally did so by dropping both and introducing a new "pax" program
to fill this role.
The "pax" program is specified to read and write both ustar and the POSIX cpio format.
The standard also introduced a new "pax interchange format" which is based on
ustar and provides a generic way to extend it with new features.

The pax interchange format is proving fairly successful; GNU tar and
many other tar programs now support it.

Detailed descriptions of Tar formats and details of libarchive's implementation
can be found on the following pages:

* [[The tar.5 man page|ManPageTar5]] provides technical details of several tar formats and extensions, including the pax interchange format.
* The [[POSIX standard for pax|http://pubs.opengroup.org/onlinepubs/9699919799/utilities/pax.html]] includes the official definitions for ustar and pax interchange format.
* [[TarExtendedAttributes]] explains some of the approaches that have been used to store "extended attribute" information in tar archives.
* [[TarPosix1eACLs]] explains how POSIX.1e ACLs have been stored.  (POSIX.1e was an early attempt to standardize ACL and other filesystem extensions.  Several systems now support ACLs based on it, although it is incomplete and was never accepted as an official POSIX standard.)
* [[TarNFS4ACLs]] explains some techniques that have been used for storing NFS4/NTFS ACLs, the limitations of these methods, and proposes a method that may be implemented in libarchive.

Trivia:  At one time, libarchive could read some "tap" and "tp" format archives.
The support was never finished simply because of a lack of sample archives to test it against.
