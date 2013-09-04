#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_INIT([mcsf],[0.0.1],[mathieu dot desnoyers at efficios dot com])

AC_CONFIG_AUX_DIR([config])
AC_CANONICAL_TARGET
AC_CANONICAL_HOST
AC_CONFIG_MACRO_DIR([config])
AM_INIT_AUTOMAKE([foreign dist-bzip2 no-dist-gzip])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])

# Configuration options, which will be installed in the config.h
AC_CONFIG_HEADERS([config.h])

# Compute minor/major/patchlevel version numbers
AC_PROG_SED
major_version=$(echo AC_PACKAGE_VERSION | sed 's/^\([[0-9]]\)*\.[[0-9]]*\.[[0-9]]*.*$/\1/')
minor_version=$(echo AC_PACKAGE_VERSION | sed 's/^[[0-9]]*\.\([[0-9]]*\)\.[[0-9]]*.*$/\1/')
patchlevel_version=$(echo AC_PACKAGE_VERSION | sed 's/^[[0-9]]*\.[[0-9]]*\.\([[0-9]]*\).*$/\1/')
AC_SUBST([MAJOR_VERSION], [$major_version])
AC_SUBST([MINOR_VERSION], [$minor_version])
AC_SUBST([PATCHLEVEL_VERSION], [$patchlevel_version])
AC_DEFINE_UNQUOTED([VERSION_MAJOR], $major_version, [UST major version number])
AC_DEFINE_UNQUOTED([VERSION_MINOR], $minor_version, [UST minor version number])
AC_DEFINE_UNQUOTED([VERSION_PATCHLEVEL], $patchlevel_version, [UST patchlevel version number])

version_name="TBD"
version_description="TBD"

AC_DEFINE_UNQUOTED([VERSION_NAME], ["$version_name"], [MCSF version name])
AC_DEFINE_UNQUOTED([VERSION_DESCRIPTION], ["$version_description"], [MCSF version description])

AC_PROG_GREP
# libtool link_all_deplibs fixup. See http://bugs.lttng.org/issues/321.
AC_ARG_ENABLE(libtool-linkdep-fixup,
	AS_HELP_STRING([--disable-libtool-linkdep-fixup],
			[disable the libtool fixup for linking all dependent libraries (link_all_deplibs)]),
	libtool_fixup=$enableval,
	libtool_fixup=yes)

AS_IF([test "x$libtool_fixup" = "xyes"],
	    [
	    libtool_m4="$srcdir/config/libtool.m4"
	    libtool_flag_pattern=".*link_all_deplibs\s*,\s*\$1\s*)"
	    AC_MSG_CHECKING([for occurence(s) of link_all_deplibs = no in $libtool_m4])
	    libtool_flag_pattern_count=$(grep -c "$libtool_flag_pattern\s*=\s*no" $libtool_m4)
	    AS_IF([test $libtool_flag_pattern_count -ne 0],
	    [
		  AC_MSG_RESULT([$libtool_flag_pattern_count])
		  AC_MSG_WARN([the detected libtool will not link all dependencies, forcing link_all_deplibs = unknown])
		  sed -i "s/\($libtool_flag_pattern\)\s*=\s*no/\1=unknown/g" $libtool_m4
		  ],
		  [
		  AC_MSG_RESULT([none])
		  ])
	    ])

# Checks for programs.
AC_PROG_CC
AC_PROG_MAKE_SET
LT_INIT

AC_CHECK_LIB([pthread], [pthread_create])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_INLINE

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([socket])

CFLAGS="-Wall $CFLAGS"

# Set compile flags to java include files if given
AC_ARG_WITH([java-jdk],
	[AS_HELP_STRING([--with-java-jdk=DIR],[use the Java JDK in DIR. Ex : $JAVA_HOME.])],
	[JAVA_JDK=$withval],
	[JAVA_JDK=""]
)
AS_IF([test $JAVA_JDK],[
	AS_IF([test -d $JAVA_JDK],[
                AC_MSG_RESULT([using Java includes in $JAVA_SDK])
                SUBDIRS=`find $JAVA_JDK/include -type d`
		CPPFLAGS+=" "
                CPPFLAGS+=`for x in $SUBDIRS; do echo -n "-I$x "; done`
		CPPFLAGS+=" "
        ],[
                AC_MSG_ERROR(Unable to find Java include files in $JAVA_JDK)
        ])
])

# where system headers are installed
mcsfincludedir="${includedir}/mcsf"
AC_SUBST(mcsfincludedir)

AC_CONFIG_FILES([
	Makefile
	src/Makefile
	src/c/Makefile
	src/c/bin/Makefile
	src/c/bin/test/Makefile
	src/c/lib/Makefile
	src/c/lib/test/Makefile
	src/c/include/Makefile
	src/c/include/mcsf/Makefile
	src/c/include/mcsf-private/Makefile
	src/java/Makefile
	doc/Makefile
	doc/examples/Makefile
	doc/man/Makefile
	tests/Makefile
	tests/unit/Makefile
	tests/unit/c/Makefile
	tests/unit/java/Makefile
	tests/regression/Makefile
])

AC_OUTPUT

AS_ECHO()
AS_ECHO("Version name: $version_name")
AS_ECHO("$version_description")

AS_ECHO()
AS_ECHO("Type 'make' to compile.")

