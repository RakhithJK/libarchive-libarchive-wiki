Directory of documentation included with the libarchive distribution.

The libarchive distribution includes full documentation
in the form of Unix-style "man pages."
These documents are included in the libarchive distribution in the following formats:
BSD mdoc, Unix man, PDF, plain text, and HTML.

* [bsdtar.1](https://www.freebsd.org/cgi/man.cgi?query=bsdtar&sektion=1&format=html) - The bsdtar command-line program
* [bsdcpio.1](https://www.freebsd.org/cgi/man.cgi?query=bsdcpio&sektion=1&format=html) - The bsdcpio command-line program
* [libarchive.3](https://www.freebsd.org/cgi/man.cgi?query=libarchive&sektion=3&format=html) - An overview of libarchive (Also see the [[Examples]], [[FormatDetection]], and [[ZeroCopy]] articles.)
* [libarchive_formats.5](https://www.freebsd.org/cgi/man.cgi?query=libarchive_formats&sektion=5&format=html) - An overview of the formats supported by libarchive
* [libarchive_changes.3](https://www.freebsd.org/cgi/man.cgi?query=libarchive_changes&sektion=3&format=html) - Differences from past releases
* [archive_entry.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry&sektion=3&format=html) - The archive_entry API used to represent entries in archives
  * [archive_entry_acl.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry_acl&sektion=3&format=html) - Details of the ACL handling for archive entries (Also see the [[TarNFS4ACLs]] and [[TarPosix1eACLs]] articles.)
  * [archive_entry_linkify.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry_linkify&sektion=3&format=html)- Details of the utility functions for detecting and managing hardlinked files
  * [archive_entry_paths.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry_paths&sektion=3&format=html) - Details of the pathname handling for archive entries
  * [archive_entry_perms.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry_perms&sektion=3&format=html) - Details of the permissions/mode storage used by archive entries
  * [archive_entry_stat.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry_stat&sektion=3&format=html) - Details of using `struct stat` with archive entries
  * [archive_entry_time.3](https://www.freebsd.org/cgi/man.cgi?query=archive_entry_time&sektion=3&format=html) - Details of the time values that can appear in archive entries
* [archive_read.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read&sektion=3&format=html) - The archive_read API used for reading from streaming archives
  * [archive_read_add_passphrase.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_add_passphrase&sektion=3&format=html) - Manage passphrases for reading encrypting archives
  * [archive_read_data.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_data&sektion=3&format=html) - Read archive entry payload
  * [archive_read_extract.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_extract&sektion=3&format=html) - Recreate archive entries on disk
  * [archive_read_filter.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_filter&sektion=3&format=html) - Configure a readable archive object with decompression filters
  * [archive_read_format.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_format&sektion=3&format=html) - Configure a readable archive object with an archive format
  * [archive_read_free.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_free&sektion=3&format=html) - Detach and deallocate a readable archive object
  * [archive_read_header.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_header&sektion=3&format=html) - Read entry metadata
  * [archive_read_new.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_new&sektion=3&format=html) - Allocate a readable archive object
  * [archive_read_open.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_open&sektion=3&format=html) - Attach a readable archive object to a data source (file, descriptor, memory ...)
  * [archive_read_set_options.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_set_options&sektion=3&format=html) - Configure filter or format driver behavior
* [archive_read_disk.3](https://www.freebsd.org/cgi/man.cgi?query=archive_read_disk&sektion=3&format=html) - The archive_read_disk API used for getting information about files (and other objects) from disk
* [archive_util.3](https://www.freebsd.org/cgi/man.cgi?query=archive_util&sektion=3&format=html) - Miscellaneous libarchive utility functions
* [archive_write.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write&sektion=3&format=html) - The archive_write API used to create streaming archives
  * [archive_write_blocksize.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_blocksize&sektion=3&format=html) - Configure block sizes for a writable archive object
  * [archive_write_data.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_data&sektion=3&format=html) - Write archive entry payload
  * [archive_write_filter.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_filter&sektion=3&format=html) - Configure a writable archive with compression filters
  * [archive_write_finish_entry.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_finish_entry&sektion=3&format=html) - Finalize a writable archive entry
  * [archive_write_format.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_format&sektion=3&format=html) - Configure a writable archive with an archive format
  * [archive_write_free.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_free&sektion=3&format=html) - Detach and deallocate a writable archive object
  * [archive_write_header.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_header&sektion=3&format=html) - Write entry metadata
  * [archive_write_new.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_new&sektion=3&format=html) - Allocate a writable archive object
  * [archive_write_open.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_open&sektion=3&format=html) - Attach a writable archive object to a data sink
  * [archive_write_set_options.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_set_options&sektion=3&format=html) - Configure filter or format driver behavior
  * [archive_write_set_passphrase.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_set_passphrase&sektion=3&format=html) - Set passphrase for writing encrypted archives
* [archive_write_disk.3](https://www.freebsd.org/cgi/man.cgi?query=archive_write_disk&sektion=3&format=html) - The archive_write_disk API used to create files (and other objects) on disk
* [tar.5](https://www.freebsd.org/cgi/man.cgi?query=tar&sektion=5&format=html) - The tar file format ("... best man page I have read in years." -- Russ Cox)
* [mtree.5](https://www.freebsd.org/cgi/man.cgi?query=mtree&sektion=5&format=html) - The mtree file format
* [cpio.5](https://www.freebsd.org/cgi/man.cgi?query=cpio&sektion=5&format=html) - The cpio file format
* [libarchive_internals.3](https://www.freebsd.org/cgi/man.cgi?query=libarchive_internals&sektion=3&format=html) - A brief survey of how libarchive works internally. (Also see the LibarchiveInternals article.)

About the numbers:  The original Unix manuals were distributed as several numbered volumes and those numbers are still used to identify categories of documentation.  The category numbers used here are:  1 is the "User Reference Manual" with documentation about command-line programs intended for use by users of the system; 3 is the "Programmer's Reference Manual" with information about programming interfaces; and 5 is the "File Formats Reference Manual" with information about the internal format of files on the system.

The Wiki formatted pages here were generated automatically from the BSD mdoc format
using the scripts in the trunk/doc directory.
Any help in improving these scripts is greatly appreciated.

Maintainers:  To update the Wiki manpages (assuming you have a checkout of the full source tree):
```bash
 $ cd trunk/doc
 $ /bin/sh update.sh
 $ cp wiki/*.wiki ../../wiki
 $ svn commit ../../wiki
```