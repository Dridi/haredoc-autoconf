AC_PREREQ([2.69])
AC_INIT([haredoc], [dev])
AC_CONFIG_SRCDIR([cmd/haredoc/main.ha])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIRS([m4])

AM_INIT_AUTOMAKE([1.12 foreign subdir-objects])
AM_MAINTAINER_MODE([disable])
AM_SILENT_RULES([yes])

LT_INIT
LT_PREREQ([2.2.6])

AC_DEFUN([HA_CHECK_PROG], [dnl
AC_ARG_VAR([$1], [$3])
AC_CHECK_PROGS([$1], [$2], [false])
AS_IF([test "$[$1]" = false], [AC_MSG_ERROR([Could not find program $2])])
])

AC_DEFUN([HA_MISSING_PROG], [dnl
AC_ARG_VAR([$1], [$3])
AM_MISSING_PROG([$1], [$2])
AC_CHECK_PROGS([$1], [$2], [false])
])

AC_DEFUN([HA_ARG_VAR], [dnl
AC_ARG_VAR([$1], [$2])
AS_IF([test -z "$ac_cv_env_[$1]_set"], [$1=$3])
AC_SUBST([$1])
])

HA_CHECK_PROG([QBE],   [qbe],   [QBE compiler backend])
HA_CHECK_PROG([HARE],  [hare],  [Hare build system])
HA_CHECK_PROG([HAREC], [harec], [Hare compiler frontend])

HA_MISSING_PROG([SCDOC], [scdoc], [manual pages generator])

HA_ARG_VAR([HAREFLAGS], [Hare build flags], [])
HA_ARG_VAR([HAREPATH],  [PATH for Hare modules],
	['${prefix}/src/hare/stdlib:${prefix}/src/hare/third-party'])

HA_ARG_VAR([AR],          [archiver])
HA_ARG_VAR([ARFLAGS],     [archiver flags])
HA_ARG_VAR([AS],          [assembler])
HA_ARG_VAR([ASFLAGS],     [assembler flags])
HA_ARG_VAR([LD],          [linker])
HA_ARG_VAR([LDLINKFLAGS], [linker flags])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
