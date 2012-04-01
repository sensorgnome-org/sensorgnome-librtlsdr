AC_INIT([librtlsdr],
        m4_esyscmd([./git-version-gen .tarball-version]),
        [osmosdr@lists.osmocom.org])

AM_INIT_AUTOMAKE([dist-bzip2])

dnl kernel style compile messages
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

dnl checks for programs
AC_PROG_MAKE_SET
AC_PROG_CC
AC_PROG_INSTALL
LT_INIT
AC_PROG_LIBTOOL

PKG_CHECK_MODULES(LIBUSB, libusb-1.0 >= 1.0)
LIBS="$LIBS $LIBUSB_LIBS"
CFLAGS="$CFLAGS $LIBUSB_CFLAGS"

AC_PATH_PROG(DOXYGEN,doxygen,false)
AM_CONDITIONAL(HAVE_DOXYGEN, test $DOXYGEN != false)

AC_CONFIG_MACRO_DIR([m4])

dnl checks for header files
AC_HEADER_STDC
AC_CHECK_HEADERS(sys/types.h)

# The following test is taken from WebKit's webkit.m4
saved_CFLAGS="$CFLAGS"
CFLAGS="$CFLAGS -fvisibility=hidden "
AC_MSG_CHECKING([if ${CC} supports -fvisibility=hidden])
AC_COMPILE_IFELSE([AC_LANG_SOURCE([char foo;])],
    [ AC_MSG_RESULT([yes])
      SYMBOL_VISIBILITY="-fvisibility=hidden"],
      AC_MSG_RESULT([no]))
CFLAGS="$saved_CFLAGS"
AC_SUBST(SYMBOL_VISIBILITY)

dnl Generate the output
AM_CONFIG_HEADER(config.h)

AC_OUTPUT(
	librtlsdr.pc
	include/Makefile
	src/Makefile
	Makefile
	Doxyfile
)