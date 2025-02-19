dnl * Copyright 2012-2014 Luke Dashjr
dnl *
dnl * This program is free software; you can redistribute it and/or modify it
dnl * under the terms of the standard MIT license.  See COPYING for more details.

AC_INIT(
	[libblkmaker],
	[0.6.0],
	[luke_libblkmaker@dashjr.org],
	[libblkmaker],
	[http://gitorious.org/bitrub/libblkmaker])
AC_CONFIG_AUX_DIR([.])
AC_PREREQ([2.59])
AM_INIT_AUTOMAKE([1.11 -Wall dist-xz foreign])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

AC_PROG_CC_C99
m4_ifdef([AM_PROG_AR], [AM_PROG_AR])
LT_INIT([disable-static])

# http://www.gnu.org/software/libtool/manual/html_node/Updating-version-info.html
AC_SUBST([LIBBLKMAKER_SO_VERSION], [8:0:0])
AC_SUBST([LIBBLKMAKER_API_VERSION], [0.1])

AC_CONFIG_FILES([Makefile
	libblkmaker_jansson-${LIBBLKMAKER_API_VERSION}.pc:libblkmaker_jansson.pc.in
])

PKG_CHECK_MODULES([JANSSON],[jansson],[
	true
],[
	AC_MSG_CHECKING([for jansson in system-default locations])
	LIBS="$LIBS -ljansson"
	AC_TRY_LINK([
		#include <jansson.h>
	],[
		json_object();
	],[
		AC_MSG_RESULT([found])
		JANSSON_LIBS=-ljansson
	],[
		AC_MSG_RESULT([not found])
		AC_MSG_ERROR([Could not find jansson library])
	])
	LIBS="${save_LIBS}"
])
AC_SUBST(JANSSON_CFLAGS)
AC_SUBST(JANSSON_LIBS)

PKG_CHECK_MODULES([libbase58],[libbase58])

AC_CHECK_LIB([ws2_32], [strchr])

dnl libgcrypt necessary to build tests and example
dnl check for libgcrypt:
m4_ifdef([AM_PATH_LIBGCRYPT], [
	AM_PATH_LIBGCRYPT([],
		[
			have_libgcrypt=yes
		],[
			have_libgcrypt=no
		])
],[
	m4_warn([syntax], [AM_PATH_LIBGCRYPT missing; example and tests will not be available])
])
AM_CONDITIONAL([HAVE_LIBGCRYPT], [test x$have_libgcrypt = xyes])

AC_OUTPUT
