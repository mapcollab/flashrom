AC_INIT([flashrom], [0.9.9-r1954m], [flashrom@flashrom.org], [flashrom], [http://www.flashrom.org/])

AC_PREREQ(2.59)

AC_CANONICAL_TARGET

AC_CONFIG_SRCDIR([flashrom.c])
AM_INIT_AUTOMAKE([dist-bzip2 no-dist-gzip tar-ustar foreign])

# Internal (mainboard) flashing
AC_ARG_WITH([internal],
	    AC_HELP_STRING([--with-internal],[mainboard internal flashing support.]),
	    [internal="$withval"],[internal="yes"])

# Needs to be disabled on Windows.
AC_ARG_WITH([serprog],
	    AC_HELP_STRING([--with-serprog],[serprog support.]),
	    [serprog="$withval"],[serprog="yes"])

AC_ARG_WITH([rayer_spi],
	    AC_HELP_STRING([--with-rayer-spi],[RayeR SPIPGM hardware support.]),
	    [rayer_spi="$withval"],[rayer_spi="yes"])

AC_ARG_WITH([pony_spi],
	    AC_HELP_STRING([--with-pony-spi],[PonyProg2000 SPI hardware support.]),
	    [pony_spi="$withval"],[pony_spi="yes"])

AC_ARG_WITH([nic3com],
	    AC_HELP_STRING([--with-nic3com],[3Com NICs support.]),
	    [nic3com="$withval"],[nic3com="yes"])

AC_ARG_WITH([gfxnvidia],
	    AC_HELP_STRING([--with-gfxnvidia],[NVIDIA graphics cards support. Note: write and erase do not work properly.]),
	    [gfxnvidia="$withval"],[gfxnvidia="yes"])

AC_ARG_WITH([satasii],
	    AC_HELP_STRING([--with-satasii],[SiI SATA controllers support.]),
	    [satasii="$withval"],[satasii="yes"])

AC_ARG_WITH([atahpt],
	    AC_HELP_STRING([--with-atahpt],[Highpoint (HPT) ATA/RAID controller support. IMPORTANT: This code is not yet working!]),
	    [atahpt="$withval"],[atahpt="no"])

AC_ARG_WITH([atavia],
	    AC_HELP_STRING([--with-atavia],[VIA VT6421A LPC programmer support.]),
	    [atavia="$withval"],[atavia="no"])

AC_ARG_WITH([it8212],
	    AC_HELP_STRING([--with-it8212],[Innovision Multimedia IT8212F PCI PATA/RAID controller support.]),
	    [it8212="$withval"],[it8212="no"])

AC_ARG_WITH([ft2232_spi],
	    AC_HELP_STRING([--with-ft2232-spi],[FT2232 SPI dongles support.]),
	    [ft2232_spi="$withval"],[ft2232_spi="yes"])

AC_ARG_WITH([dummy],
	    AC_HELP_STRING([--with-dummy],[dummy flashing support.]),
	    [dummy="$withval"],[dummy="yes"])

AC_ARG_WITH([drkaiser],
	    AC_HELP_STRING([--with-drkaiser],[Dr. Kaiser support.]),
	    [drkaiser="$withval"],[drkaiser="yes"])

AC_ARG_WITH([nicrealtek],
	    AC_HELP_STRING([--with-nicrealtek],[Realtek NICs support.]),
	    [nicrealtek="$withval"],[nicrealtek="yes"])

AC_ARG_WITH([nicnatsemi],
	    AC_HELP_STRING([--with-nicnatsemi],[National Semiconductor NICs support. Incomplete and untested.]),
	    [nicnatsemi="$withval"],[nicnatsemi="no"])

AC_ARG_WITH([nicintel],
	    AC_HELP_STRING([--with-nicintel],[Intel NICs support.]),
	    [nicintel="$withval"],[nicintel="yes"])

AC_ARG_WITH([nicintel_spi],
	    AC_HELP_STRING([--with-nicintel-spi],[SPI on Intel NICs support.]),
	    [nicintel_spi="$withval"],[nicintel_spi="yes"])

AC_ARG_WITH([nicintel_eeprom],
	    AC_HELP_STRING([--with-nicintel-eeprom],[EEPROM on Intel NICs support.]),
	    [nicintel_eeprom="$withval"],[nicintel_eeprom="yes"])


AC_ARG_WITH([gfxogp],
	    AC_HELP_STRING([--with-gfxogp],[The Open Graphics Project graphics card support.]),
	    [gfxogp="$withval"],[gfxogp="yes"])

AC_ARG_WITH([buspirate_spi],
	    AC_HELP_STRING([--with-buspirate-spi],[Bus Pirate SPI support.]),
	    [buspirate_spi="$withval"],[buspirate_spi="yes"])

AC_ARG_WITH([usbblaster_spi],
	    AC_HELP_STRING([--with-usbblaster-spi],[Altera USB-Blaster dongles support.]),
	    [usbblaster_spi="$withval"],[usbblaster_spi="yes"])

AC_ARG_WITH([dediprog],
	    AC_HELP_STRING([--with-dediprog],[Dediprog SF100 support. Incomplete and untested.]),
	    [dediprog="$withval"],[dediprog="no"])

AC_ARG_WITH([satamv],
	    AC_HELP_STRING([--with-satamv],[Marvell SATA controllers support.]),
	    [satamv="$withval"],[satamv="yes"])

AC_ARG_WITH([dmidecode],
	    AC_HELP_STRING([--with-dmidecode],[Enable dmidecode (only for x86/x86_64).]),
	    [dmidecode="$withval"],[dmidecode="yes"])
AC_ARG_WITH([dmidecode_ext],
	    AC_HELP_STRING([--with-dmidecode-external],[Use external dmidecode utility instead of internal one (only for x86/x86_64).]),
	    [dmidecode_ext="$withval"],[dmidecode_ext="yes"])

# Specific for Flashrom Wiki
AC_ARG_WITH([print_wiki],
	    AC_HELP_STRING([--with-print-wiki],[enable wiki export support. It is only useful if you have Flashrom wiki access.]),
	    [print_wiki="$withval"],[print_wiki="no"])

AC_C_BIGENDIAN(
	       [AC_DEFINE([__FLASHROM_BIG_ENDIAN__], [1], [Big endian])],
	       [AC_DEFINE([__FLASHROM_LITTLE_ENDIAN__], [1], [Little endian])],
	       [AC_MSG_ERROR([Unknown endianness])],
	       [AC_MSG_ERROR([No support for universal binaries yet])]
	       )

# Check for CPU-specific features
case "$target_cpu" in
	i386|i486|i586|i686|i786|x86_64)
		if test "$internal" = 'yes'; then
			enable_x86_only_internal="yes"
		else
			enable_x86_only_internal="no"
		fi

		AC_CHECK_HEADERS([sys/io.h])

		if test "$dmidecode_ext" = 'yes'; then
			AC_PATH_PROG([DMIDECODE], dmidecode, [], [$PATH$PATH_SEPARATOR/usr/sbin])
		fi

		;;
	mips*|power*|arm*)
		enable_x86_only_internal="n/a"
		if test "$nic3com" = 'yes'; then
			AC_MSG_WARN([NIC 3Com is not supported for this target ($target_cpu). No PCI port I/O access on this architecture yet.])
			nic3com="no"
		fi
		if test "$nicnatsemi" = 'yes'; then
			AC_MSG_WARN([NIC NatSemi is not supported for this target ($target_cpu). No PCI port I/O access on this architecture yet.])
			nicnatsemi="no"
		fi
		if test "$nicrealtek" = 'yes'; then
			AC_MSG_WARN([NIC Realtek is not supported for this target ($target_cpu). No PCI port I/O access on this architecture yet.])
			nicrealtek="no"
		fi
		if test "$rayer_spi" = 'yes'; then
			AC_MSG_WARN([RayeR SPIPGM is not supported for this target ($target_cpu). No PCI port I/O access on this architecture yet.])
			rayer_spi="no"
		fi
		if test "$satamv" = 'yes'; then
			AC_MSG_WARN([Marvell SATA is not supported for this target ($target_cpu). No PCI port I/O access on this architecture yet])
			satamv="no"
		fi
		if test "$atahpt" = 'yes'; then
			AC_MSG_WARN([Highpoint (HPT) ATA/RAID controller support is not supported for this target ($target_cpu). No PCI port I/O access on this architecture yet.])
			atahpt="no"
		fi
		if test "$dmidecode" = 'yes' -o "$dmidecode_ext" = 'yes' ; then
			AC_MSG_WARN([DMI handling is not supported for this target ($target_cpu).])
			dmidecode="no"
			dmidecode_ext=""
		fi
		;;
	*)
		AC_MSG_ERROR([No support for this CPU ($target_cpu) yet])
		;;
esac

# Enable OS-specific compilation flags
case "$target_os" in
	linux*)
		AC_CHECK_HEADERS([sys/ioctl.h])
		AC_ARG_WITH(
			    [linux_spi],
			    AC_HELP_STRING([--with-linux-spi],[Linux SPI subsystem support.]),
			    [linux_spi="$withval"],
			    [linux_spi="yes"]
			    )
		if test "$linux_spi" = "yes" ; then
			AC_CHECK_HEADERS([linux/types.h], [], [AC_MSG_ERROR([<linux/types.h> not found])], [])
			AC_CHECK_HEADERS([linux/spi/spidev.h], [], [AC_MSG_ERROR([<linux/spi/spidev.h> not found])], [])
		fi
		;;
	darwin*)
		linux_spi="n/a"
		AC_CHECK_HEADERS([DirectIO/darwinio.h DirectHW/DirectHW.h])
		;;
	freebsd*)
		linux_spi="n/a"
		AC_CHECK_HEADERS([machine/cpufunc.h])
		;;
	openbsd*)
		linux_spi="n/a"
		AC_CHECK_HEADERS([machine/sysarch.h sys/types.h])
		;;
	netbsd*)
		linux_spi="n/a"
		AC_CHECK_HEADERS([machine/sysarch.h sys/types.h])
		;;
	*solaris*)
		linux_spi="n/a"
		AC_CHECK_HEADERS([asm/sunddi.h strings.h sys/psw.h sys/sysi86.h])
		;;
	mingw*)
		linux_spi="n/a"
		# MinGW doesn't have the ffs() function, but we can use gcc's __builtin_ffs().
		CFLAGS="$CFLAGS -Dffs=__builtin_ffs"
		# Some functions provided by Microsoft do not work as described in C99 specifications. This macro fixes that
		# for MinGW. See http://sourceforge.net/apps/trac/mingw-w64/wiki/printf%20and%20scanf%20family */
		CFLAGS="$CFLAGS -D__USE_MINGW_ANSI_STDIO=1"
		;;
	*djgpp*)
		linux_spi="n/a"
		AC_CHECK_HEADERS([pc.h])
		# DJGPP has odd uint*_t definitions which cause lots of format string warnings.
		CFLAGS="$CFLAGS -Wno-format"
		;;
	*)
		AC_MSG_ERROR([No support for this OS ($target_os) yet])
		;;
esac

# Check whether we need serial support
if test "$serprog" = 'yes' -o \
	"$buspirate_spi" = 'yes' -o \
	"$pony_spi" = 'yes' ; then
	serial="yes"
else
	serial="no"
fi

# Check whether we need PCI support
if test "$internal" = 'yes' -o \
	"$rayer_spi" = 'yes' -o \
	"$nic3com" = 'yes' -o \
	"$gfxnvidia" = 'yes' -o \
	"$satasii" = 'yes' -o \
	"$atahpt" = 'yes' -o \
	"$atavia" = 'yes' -o \
	"$it8212" = 'yes' -o \
	"$drkaiser" = 'yes' -o \
	"$nicrealtek" = 'yes' -o \
	"$nicnatsemi" = 'yes' -o \
	"$nicintel" = 'yes' -o \
	"$nicintel_spi" = 'yes' -o \
	"$nicintel_eeprom" = 'yes' -o \
	"$gfxogp" = 'yes' -o \
	"$satamv" = 'yes' ; then
	pci="yes"
fi

if test "$rayer_spi" = 'yes' -o \
	"$pony_spi" = 'yes' -o \
	"$internal" = 'yes' -o \
	"$nicintel_spi" = 'yes' -o \
	"$gfxogp" = 'yes' ; then
	bitbang_spi="yes"
else
	bitbang_spi="no"
fi

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

# Checks for header files.
AC_CHECK_HEADERS([limits.h stddef.h stdint.h stdlib.h string.h sys/time.h sys/utsname.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE
AC_TYPE_OFF_T
AC_TYPE_SIZE_T
AC_CHECK_SIZEOF(int)
dnl mingw (for instance) lacks ssize_t
AC_CHECK_TYPE(ssize_t, int)
AC_CHECK_TYPE(uint8_t, unsigned char)
AC_CHECK_TYPE(uint16_t, unsigned short)
AC_CHECK_TYPE(uint64_t, unsigned long long)
if test $ac_cv_sizeof_int -eq 4 ; then
AC_CHECK_TYPE(uint32_t, unsigned int)
elif test $ac_cv_size_long -eq 4 ; then
AC_CHECK_TYPE(uint32_t, unsigned long)
else
AC_MSG_ERROR([no 32-bit type found])
fi

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_MMAP
AC_FUNC_REALLOC
AC_CHECK_FUNCS([getpagesize gettimeofday memmove memset munmap strcasecmp strchr strcspn strdup strerror strncasecmp strspn strstr strtol strtoul uname])

# Checks for pcilib
if test "$pci" = 'yes' ; then
	AC_CHECK_LIB([pci], [pci_alloc],,[AC_MSG_ERROR([pci library missing])])
fi

# check for socket (required for SunOS)
if test "$serprog" = 'yes' ; then
	AC_CHECK_LIB([socket], [socket])
	AC_CHECK_HEADERS([arpa/inet.h fcntl.h inttypes.h netdb.h netinet/in.h sys/socket.h termios.h unistd.h])
	AC_CHECK_FUNCS([gethostbyaddr gethostbyname socket])
fi

# Check for libusb
if test "$dediprog" = 'yes' -o "$ft2232_spi" = 'yes'  ; then
	AC_CHECK_LIB([usb], [usb_init])
fi

if test "$ft2232_spi" = 'yes' -o "$usbblaster_spi" = 'yes' ; then
	AC_CHECK_HEADERS([ftdi.h],[],[AC_MSG_ERROR([<ftdi.h> header not found])],[AC_INCLUDES_DEFAULT])
	AC_CHECK_LIB([ftdi],[ftdi_init],,[AC_MSG_ERROR([ftdi library is missing])])
fi

# For Makefile.am
AM_CONDITIONAL(HAVE_INTERNAL, test "$internal" = "yes")
AM_CONDITIONAL(HAVE_DMIDECODE, test "$dmidecode" = "yes")
AM_CONDITIONAL(HAVE_DMIDECODE_EXT, test "$DMIDECODE" != "")
AM_CONDITIONAL(HAVE_X86_ONLY_INTERNAL, test "$enable_x86_only_internal" = "yes")
AM_CONDITIONAL(HAVE_SERPROG, test "$serprog" = "yes")
AM_CONDITIONAL(HAVE_LINUX_SPI, test "$linux_spi" = "yes")
AM_CONDITIONAL(HAVE_RAYER_SPI, test "$rayer_spi" = "yes")
AM_CONDITIONAL(HAVE_PONY_SPI, test "$pony_spi" = "yes")
AM_CONDITIONAL(HAVE_BITBANG_SPI, test "$bitbang_spi" = "yes")
AM_CONDITIONAL(HAVE_NIC3COM, test "$nic3com" = "yes")
AM_CONDITIONAL(HAVE_GFXNVIDIA, test "$gfxnvidia" = "yes")
AM_CONDITIONAL(HAVE_SATASII, test "$satasii" = "yes")
AM_CONDITIONAL(HAVE_ATAHPT, test "$atahpt" = "yes")
AM_CONDITIONAL(HAVE_ATAVIA, test "$atavia" = "yes")
AM_CONDITIONAL(HAVE_IT8212, test "$it8212" = "yes")
AM_CONDITIONAL(HAVE_FT2232_SPI, test "$ft2232_spi" = "yes")
AM_CONDITIONAL(HAVE_DUMMY, test "$dummy" = "yes")
AM_CONDITIONAL(HAVE_DRKAISER, test "$drkaiser" = "yes")
AM_CONDITIONAL(HAVE_NICREALTEK, test "$nicrealtek" = "yes")
AM_CONDITIONAL(HAVE_NICNATSEMI, test "$nicnatsemi" = "yes")
AM_CONDITIONAL(HAVE_NICINTEL, test "$nicintel" = "yes")
AM_CONDITIONAL(HAVE_NICINTEL_SPI, test "$nicintel_spi" = "yes")
AM_CONDITIONAL(HAVE_NICINTEL_EEPROM, test "$nicintel_eeprom" = "yes")
AM_CONDITIONAL(HAVE_GFXOGP, test "$gfxogp" = "yes")
AM_CONDITIONAL(HAVE_BUSPIRATE_SPI, test "$buspirate_spi" = "yes")
AM_CONDITIONAL(HAVE_USBBLASTER_SPI, test "$usbblaster_spi" = "yes")
AM_CONDITIONAL(HAVE_DEDIPROG, test "$dediprog" = "yes")
AM_CONDITIONAL(HAVE_SATAMV, test "$satamv" = "yes")
AM_CONDITIONAL(HAVE_SERIAL, test "$serial" = "yes")
AM_CONDITIONAL(HAVE_PCI, test "$pci" = "yes")
AM_CONDITIONAL(HAVE_PRINT_WIKI, test "$print_wiki" = "yes")

AC_CONFIG_FILES([Makefile])
AC_OUTPUT

AC_MSG_RESULT([
------------------------------------------------------------------------
  $PACKAGE $VERSION configuration.

    Compiler support:

      Target CPU: ................... ${target_cpu}
      Target OS: .................... ${target_os}

    Suppored programmers:

      Internal: ..................... ${internal}
        x86-only features: .......... ${enable_x86_only_internal}
      serprog: ...................... ${serprog}
      Linux SPI: .................... ${linux_spi}
      RayeR SPI: .................... ${rayer_spi}
      PonyProg2000 SPI: ............. ${pony_spi}
      Bitbang SPI: .................. ${bitbang_spi}
      3COM NIC: ..................... ${nic3com}
      NVIDIA GFX: ................... ${gfxnvidia}
      Silicon Image SATA: ........... ${satasii}
      Highpoint ATA: ................ ${atahpt}
      VIA VT6421A LPC: .............. ${atavia}
      IT8212F PCI PATA/RAID: ........ ${it8212}
      FT232 SPI: .................... ${ft2232_spi}
      Dummy: ........................ ${dummy}
      Dr. Kaiser: ................... ${drkaiser}
      Realtek NIC: .................. ${nicrealtek}
      National Semiconductor NIC: ... ${nicnatsemi}
      Intel NIC: .................... ${nicintel}
      Intel NIC SPI: ................ ${nicintel_spi}
      Intel NIC EEPROM: ............. ${nicintel_eeprom}
      Open Graphics Project GFX: .... ${gfxogp}
      Bus Pirate SPI: ............... ${buspirate_spi}
      Altera USB-Blaster SPI: ....... ${usbblaster_spi}
      Dediprog SF100: ............... ${dediprog}
      Marvell SATA: ................. ${satamv}
      Serial: ....................... ${serial}

------------------------------------------------------------------------
])
