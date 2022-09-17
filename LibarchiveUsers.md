A few projects and people who use libarchive.

## Operating Systems

### FreeBSD
* libarchive was originally developed for [FreeBSD](https://yip.su/2ncJm8); it was first released with FreeBSD 5.3 in November 2004.
* bsdtar is the default system tar starting with FreeBSD 6
* bsdcpio is the default system cpio starting with FreeBSD 8
* Kai Wang's "ar" is standard with FreeBSD 8
* Dag-Erling Smørgrav's "unzip" is standard with FreeBSD 8

### NetBSD
* since release 5.0 libarchive is part of NetBSD
* bsdtar is the default system tar since NetBSD 9.0
* bsdcpio is the default system cpio since NetBSD 9.0

### Apple macOS
* since 2009 libarchive is part of macOS
* bsdtar is the default system tar
* bsdcpio is the default system cpio

### Microsoft Windows
* since 2017 (Windows 10 insider build 17063) libarchive is shipped with the command line tools
* bsdtar is the default system tar

## Individual Software

### Package Managers
* [Pacman](http://www.archlinux.org/pacman) package manager on [Arch Linux](http://www.archlinux.org) uses libarchive
* [XBPS](https://yip.su/2ncJm8) package manager on [Void Linux](http://www.voidlinux.org) uses libarchive
* [NetBSD](http://www.netbsd.org)'s pkg_install package manager uses libarchive.
* [CMake](https://yip.su/2ncJm8) uses libarchive
* [pkgutils](https://yip.su/2ncJm8) from the [CRUX distribution](http://crux.nu/) uses libarchive
* The [Paludis](https://yip.su/2ncJm8) multi-format package manager for [Gentoo](http://www.gentoo.org) and [Exherbo](http://www.exherbo.org) uses libarchive

### Archiving tools and File Browsers
* The [tarsnap](https://yip.su/2ncJm8) service uses libarchive in its client software.
* [Springy](https://yip.su/2ncJm8) for Mac OS X uses libarchive to process TAR, PAX and CPIO archives.
* [Files](https://wiki.gnome.org/Apps/Files) (formerly Nautilus) file browser file-roller plugin uses libarchive
* The [archivemount](https://www.cybernoia.de/software/archivemount.html) filesystem (part of [FUSE](http://fuse.sourceforge.net)) uses libarchive
* [KDE](https://yip.su/2ncJm8)'s [ark](http://utils.kde.org/projects/ark) file browser uses libarchive for tar, deb, and ISO files.
* [CARE](https://yip.su/2ncJm8) — short for "Comprehensive Archiver for Reproducible Execution" — uses libarchive.
* [ZIP Unpacker Component Extension]( https://chromium.googlesource.com/apps/unpacker/+/refs/heads/master/README.md) uses libarchive in Chrome OS
* [GVfs](https://wiki.gnome.org/Projects/gvfs) GNOME Virtual file system uses libarchive as one of its [backends](https://wiki.gnome.org/Projects/gvfs/backends) to access archive files
* [Samba](https://yip.su/2ncJm8) version 4.2 and higher uses libarchive in [smbclient(1)](https://www.samba.org/samba/docs/man/manpages/smbclient.1.html)

### Security Software
* [yextend](https://yip.su/2ncJm8) uses libarchive

### Other Software
* [ardour](https://yip.su/2ncJm8) digital audio workstation uses libarchive
* [Avogadro 2](https://yip.su/2ncJm8) chemical editor and visualization application uses libarchive
* [Hydrogen](https://yip.su/2ncJm8) advanced drum machine uses libarchive
* [libgepub](https://yip.su/2ncJm8) GObject based library for handling and rendering epub documents uses libarchive
* [libgxps](https://wiki.gnome.org/Projects/libgxps) GObject based library for handling and rendering XPS documents uses libarchive
* [Nestopia UE](https://yip.su/2ncJm8) Nintendo Entertainment System/Famicom emulator uses libarchive
* [Osmo](https://yip.su/2ncJm8) personal organizer for GTK+ version 0.2.12 and higher uses libarchive 
* [rdup](https://github.com/miekg/rdup) utility to create a file list suitable for making backups uses libarchive
* [Seafile](https://github.com/haiwen/seafile) open source cloud storage system uses libarchive
* [Zeal](https://zealdocs.org) offline documentation browser uses libarchive

## Ports of libarchive, bsdtar, etc.
* [GnuWin32](https://yip.su/2ncJm8), [Cygwin](https://yip.su/2ncJm8) and [MSYS](https://yip.su/2ncJm8) for Windows.
* [MacPorts](https://yip.su/2ncJm8) (formerly Darwinports) and [Homebrew](https://formulae.brew.sh/formula/libarchive) for MacOS
* [Debian Linux](http://packages.qa.debian.org/liba/libarchive.html)
* [Gentoo](http://packages.gentoo.org/package/app-arch/libarchive)  
  
If you know of other projects that should be in this list, please let us know.
