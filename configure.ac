#     $Id: configure.in,v 1.27 2003/06/22 02:15:10 robs Exp $
#
#     This file is an input file used by the GNU "autoconf" program to
#     generate the file "configure", which is run during the build
#     to configure the system for the local environment.

AC_INIT(libfcgi, 2.4.1-wmo2)
AM_INIT_AUTOMAKE([1.11 foreign])
AM_SILENT_RULES([yes])
AM_CONFIG_HEADER(include/fcgi_config.h)

AC_CONFIG_MACRO_DIRS([m4])
AC_CONFIG_FILES([Makefile
                 cgi-fcgi/Makefile
                 include/Makefile
                 src/Makefile
                 examples/Makefile
                 fcgi.pc
                 fcgi++.pc])

AC_PROG_CC
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LIBTOOL

AC_PROG_CXX

AC_LANG([C++])

# autoconf defaults CXX to 'g++', so its unclear whether it exists/works
AC_MSG_CHECKING([whether $CXX works])
AC_TRY_COMPILE([#include <iostream>],
               [std::cout << "ok";],
               [AC_MSG_RESULT(yes)
                LIBFCGIXX=libfcgi++.la
                ECHO_CPP=echo-cpp${EXEEXT}
                AC_MSG_CHECKING([whether cin has a streambuf assignment operator])
                AC_TRY_COMPILE([#include <iostream>],
                               [cin = static_cast<streambuf *>(0);],
                               [AC_MSG_RESULT(yes)
                                AC_DEFINE([HAVE_IOSTREAM_WITHASSIGN_STREAMBUF],  [1],
                                          [Define if cin/cout/cerr has a streambuf assignment operator])],
                               [AC_MSG_RESULT(no)])
                AC_MSG_CHECKING([whether char_type is defined in the context of streambuf])
                AC_TRY_COMPILE([#include <iostream>],
                               [class fcgi_streambuf : public std::streambuf { char_type ct; }],
                               [AC_MSG_RESULT(yes)
                                AC_DEFINE([HAVE_STREAMBUF_CHAR_TYPE], [1],
                                          [Define if char_type is defined in the context of streambuf])],
                               [AC_MSG_RESULT(no)])],
               [AC_MSG_RESULT(no)])
AC_SUBST(LIBFCGIXX)
AC_SUBST(ECHO_CPP)

AC_LANG([C])

AC_CHECK_LIB([nsl],       [gethostbyname])
AC_CHECK_LIB([socket],    [socket])

ACX_PTHREAD([THREADED=threaded${EXEEXT}])
AC_SUBST([THREADED])

FCGI_COMMON_CHECKS

AC_REPLACE_FUNCS([strerror])

AC_C_INLINE

#--------------------------------------------------------------------
#  This is a little hokie in that it avoids including config.guess
#  and config.sub in the distribution, but its been working so far.
#  Windows builds don't run configure so we should be safe fixing
#  this to 'unix' (at least for now).
#--------------------------------------------------------------------
SYSTEM=unix
AC_SUBST([SYSTEM])

AC_PROG_CC_WARNINGS

# Optional features
AC_ARG_ENABLE([examples],
	[AC_HELP_STRING([--enable-examples], [Build fcgi examples])],
	[], [enable_examples=no])
AM_CONDITIONAL([ENABLE_EXAMPLES], [test "$enable_examples" = yes])

AC_ARG_ENABLE([cgi],
	[AC_HELP_STRING([--enable-cgi], [Build fcgi cgi-fcgi wrapper])],
	[], [enable_cgi=no])
AM_CONDITIONAL([ENABLE_CGI], [test "$enable_cgi" = yes])

AC_ARG_WITH([pkgconfigdir],
  [AS_HELP_STRING([--with-pkgconfigdir=DIR], [pkgconfig files])],
  [pkgconfigdir=$withval],
  [pkgconfigdir="\${libdir}/pkgconfig"])
AC_SUBST([pkgconfigdir], [$pkgconfigdir])

AC_OUTPUT
