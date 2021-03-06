AC_INIT(armadito-mod-h1, [0.12.7], fdechelle@teclib.com)
AM_INIT_AUTOMAKE([foreign])

# collect arguments
# debug
AC_ARG_ENABLE([debug],
	AS_HELP_STRING([--enable-debug],[enable debugging @<:@default is yes@:>@]),
	,
	enable_debug="yes")

# database directory
AC_ARG_WITH([dbdir],
	AS_HELP_STRING([--with-dbdir=DIR],[specify path to databases @<:@default is /var/lib/armadito/bases/moduleH1@:>@]),

	with_dbdir="$withval",
	with_dbdir="no")

# check for analysis module sources
AC_MSG_CHECKING(for analysis module sources)
AC_CONFIG_SRCDIR(src/lib/src/h1-static.c)
AC_MSG_RESULT(yes)

# check for needed programs
AC_PROG_CC([gcc])
AC_PROG_LIBTOOL

# start with clean CFLAGS
CFLAGS=

# check for debug
AC_MSG_CHECKING(for debug)
AC_MSG_RESULT($enable_debug)
AM_CONDITIONAL([DEBUG], [test "$enable_debug" = "yes"])
if test "$enable_debug" = "yes"; then
   AC_DEFINE(DEBUG,1,[Define DEBUG to enable debug messages])
   CFLAGS="${CFLAGS} -g"
fi

PKG_PROG_PKG_CONFIG

# check for libarmadito
PKG_CHECK_MODULES(LIBARMADITO, libarmadito, [HAVE_LIBARMADITO=yes], [HAVE_LIBARMADITO=no])
if test "$HAVE_LIBARMADITO" = "no"; then
   AC_MSG_ERROR("cannot find ARMADITO library")
fi

# database directory
AC_MSG_CHECKING(for databases directory)
if test "$with_dbdir" = "no" ; then
   MODULEH1_DBDIR="$localstatedir/lib/armadito/bases/moduleH1"
else
   MODULEH1_DBDIR="$with_dbdir"
fi
AC_MSG_RESULT($MODULEH1_DBDIR)
if test ! -f "$MODULEH1_DBDIR/linux/database.elfdata" ; then
   AC_MSG_WARN("cannot find $MODULEH1_DBDIR/linux/database.elfdata, continuing anyway")
fi
AC_SUBST(MODULEH1_DBDIR)

# Output files
AC_CONFIG_FILES([
Makefile
src/Makefile
conf/Makefile
])
AC_OUTPUT
