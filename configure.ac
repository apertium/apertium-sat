AC_PREREQ(2.52)

AC_INIT([Apertium Santali], [0.1.0], [prasantahembram720@gmail.com], [apertium-sat], [https://wiki.apertium.org/wiki/Apertium-sat])
AM_INIT_AUTOMAKE
AC_PROG_AWK

PKG_CHECK_MODULES(APERTIUM, apertium >= 3.8.0)
PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox >= 3.6.0)
PKG_CHECK_MODULES(CG3, cg3 >= 1.3.1)

PKG_CHECK_MODULES(REGTEST, apertium-regtest >= 0.0.1, [],
                  [AC_MSG_WARN([Running tests requires apertium-regtest])])

AP_MKINCLUDE

AC_OUTPUT([Makefile apertium-sat.pc])
