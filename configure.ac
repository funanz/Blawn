#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([blawn], [1.0.0])
AC_CONFIG_SRCDIR([src])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE([1.9 foreign])
AM_SILENT_RULES([yes])

AC_ARG_VAR([PYTHON3], [Set another Python.])
AC_ARG_VAR([LLVM_CONFIG], [Set another llvm-config.])

# Checks for programs.
AC_PROG_YACC
AC_PROG_LEX
AC_PROG_CXX
AC_PROG_CC
AC_PROG_LIBTOOL

AC_CHECK_PROG(READLINK, readlink, readlink)
if test -z "$READLINK"; then
    AC_MSG_ERROR([could not find readlink])
fi

PYTHON3_LIST="python3 python3.9 python3.8 python3.7 python3.6 python3.5"

AC_PATH_PROGS(PYTHON3, $PYTHON3_LIST)
if test -z "$PYTHON3"; then
    AC_MSG_ERROR([could not find python3])
fi

LLVM_CONFIG_LIST="llvm-config llvm-config-9 llvm-config-90
                  llvm-config-8 llvm-config-80 llvm-config-7
                  llvm-config-70 llvm-config-6 llvm-config-60
                  llvm-config-5 llvm-config-50"

AC_CHECK_PROGS(LLVM_CONFIG, $LLVM_CONFIG_LIST)
if test -z "$LLVM_CONFIG"; then
    AC_MSG_ERROR([could not find llvm-config])
fi

AC_SUBST([LLVM_CXXFLAGS], `$LLVM_CONFIG --cxxflags`)
AC_SUBST([LLVM_LDFLAGS], `$LLVM_CONFIG --ldflags`)
AC_SUBST([LLVM_BINDIR], `$LLVM_CONFIG --bindir`)
AC_SUBST([LLVM_LIBS], `$LLVM_CONFIG --libs core`)
AC_SUBST([LLVM_LIBDIR], `$LLVM_CONFIG --libdir`)

AC_PATH_PROG(LLVM_LLC, llc, "", $LLVM_BINDIR)
if test -z "$LLVM_LLC"; then
    AC_MSG_ERROR([could not find llc])
fi

AC_PATH_PROG(CLANG, clang, "", $LLVM_BINDIR)
if test -z "$CLANG"; then
    AC_MSG_ERROR([could not find clang])
fi

# Checks for libraries.
LIBCLANG=$LLVM_LIBDIR/libclang.so
AC_MSG_CHECKING([for libclang])
if test -L "$LIBCLANG"; then
    AC_SUBST([LLVM_LIBCLANG], `$READLINK -f $LIBCLANG`)
    AC_MSG_RESULT([$LLVM_LIBCLANG])
else
    AC_MSG_RESULT([no])
    AC_MSG_ERROR([could not find $LIBCLANG])
fi

AC_MSG_CHECKING([for libstdc++fs])
AC_LANG_PUSH(C++)
LIBS_SAVE=$LIBS
LIBCXXFS_LIST="-lstdc++fs -lc++experimental"
for i in $LIBCXXFS_LIST; do
    LIBS=$i
    AC_TRY_LINK([], [], LIBCXXFS=$i)
    test -n "$LIBCXXFS" && break
done
if test -z "$LIBCXXFS"; then
    AC_MSG_RESULT([no])
    AC_MSG_ERROR([could not find libstdc++fs])
else
    AC_MSG_RESULT([$LIBCXXFS])
    AC_SUBST([LIBCXXFS])
fi
LIBS=$LIBS_SAVE
AC_LANG_POP(C++)

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_CONFIG_FILES([Makefile src/compiler/Makefile src/libs/Makefile])
AC_CONFIG_FILES([src/libs/cridge], [chmod +x src/libs/cridge])

AC_OUTPUT
