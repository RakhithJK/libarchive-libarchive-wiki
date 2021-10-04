A few projects and people who use libarchive.

## Operating Systems

### FreeBSD
* libarchive was originally developed for [FreeBSD](http://freebsd.org); it was first released with FreeBSD 5.3 in November 2004.
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
* [XBPS](http://www.voidlinux.org/xbps) package manager on [Void Linux](http://www.voidlinux.org) uses libarchive
* [NetBSD](http://www.netbsd.org)'s pkg_install package manager uses libarchive.
* [CMake](http://cmake.org) uses libarchive
* [pkgutils](http://crux.nu/gitweb/?p=tools/pkgutils.git) from the [CRUX distribution](http://crux.nu/) uses libarchive
* The [Paludis](http://paludis.pioto.org) multi-format package manager for [Gentoo](http://www.gentoo.org) and [Exherbo](http://www.exherbo.org) uses libarchive

### Archiving tools and File Browsers
* The [tarsnap](http://www.tarsnap.com) service uses libarchive in its client software.
* [Springy](https://www.macupdate.com/app/mac/22103/springy) for Mac OS X uses libarchive to process TAR, PAX and CPIO archives.
* [Files](https://wiki.gnome.org/Apps/Files) (formerly Nautilus) file browser file-roller plugin uses libarchive
* The [archivemount](https://www.cybernoia.de/software/archivemount.html) filesystem (part of [FUSE](http://fuse.sourceforge.net)) uses libarchive
* [KDE](http://kde.org)'s [ark](http://utils.kde.org/projects/ark) file browser uses libarchive for tar, deb, and ISO files.
* [CARE](https://github.com/proot-me/proot) — short for "Comprehensive Archiver for Reproducible Execution" — uses libarchive.
* [ZIP Unpacker Component Extension]( https://chromium.googlesource.com/apps/unpacker/+/refs/heads/master/README.md) uses libarchive in Chrome OS
* [GVfs](https://wiki.gnome.org/Projects/gvfs) GNOME Virtual file system uses libarchive as one of its [backends](https://wiki.gnome.org/Projects/gvfs/backends) to access archive files
* [Samba](https://www.samba.org) version 4.2 and higher uses libarchive in [smbclient(1)](https://www.samba.org/samba/docs/man/manpages/smbclient.1.html)

### Security Software
* [yextend](https://github.com/BayshoreNetworks/yextend) uses libarchive

### Other Software
* [ardour](https://ardour.org) digital audio workstation uses libarchive
* [Avogadro 2](https://www.openchemistry.org/projects/avogadro2) chemical editor and visualization application uses libarchive
* [Hydrogen](http://www.hydrogen-music.org) advanced drum machine uses libarchive
* [libgepub](https://github.com/danigm/libgepub) GObject based library for handling and rendering epub documents uses libarchive
* [libgxps](https://wiki.gnome.org/Projects/libgxps) GObject based library for handling and rendering XPS documents uses libarchive
* [Nestopia UE](http://0ldsk00l.ca/nestopia) Nintendo Entertainment System/Famicom emulator uses libarchive
* [Osmo](http://clayo.org/osmo) personal organizer for GTK+ version 0.2.12 and higher uses libarchive 
* [rdup](https://github.com/miekg/rdup) utility to create a file list suitable for making backups uses libarchive
* [Seafile](https://github.com/haiwen/seafile) open source cloud storage system uses libarchive
* [Zeal](https://zealdocs.org) offline documentation browser uses libarchive

## Ports of libarchive, bsdtar, etc.
* [GnuWin32](http://gnuwin32.sourceforge.net), [Cygwin](http://cygwin.org) and [MSYS](http://www.msys2.org) for Windows.
* [MacPorts](https://ports.macports.org/port/libarchive/summary) (formerly Darwinports) and [Homebrew](https://formulae.brew.sh/formula/libarchive) for MacOS
* [Debian Linux](http://packages.qa.debian.org/liba/libarchive.html)
* [Gentoo](http://packages.gentoo.org/package/app-arch/libarchive)  
  
If you know of other projects that should be in this list, please let us know.
