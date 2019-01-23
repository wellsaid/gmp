## Process this file with automake to generate Makefile.in


# Copyright 1991, 1993, 1994, 1996, 1997, 1999-2004, 2006-2009, 2011-2016 Free
# Software Foundation, Inc.
#
#  This file is part of the GNU MP Library.
#
#  The GNU MP Library is free software; you can redistribute it and/or modify
#  it under the terms of either:
#
#    * the GNU Lesser General Public License as published by the Free
#      Software Foundation; either version 3 of the License, or (at your
#      option) any later version.
#
#  or
#
#    * the GNU General Public License as published by the Free Software
#      Foundation; either version 2 of the License, or (at your option) any
#      later version.
#
#  or both in parallel, as here.
#
#  The GNU MP Library is distributed in the hope that it will be useful, but
#  WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
#  or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
#  for more details.
#
#  You should have received copies of the GNU General Public License and the
#  GNU Lesser General Public License along with the GNU MP Library.  If not,
#  see https://www.gnu.org/licenses/.


# The following options are the same as AM_INIT_AUTOMAKE in configure.in,
# except no $(top_builddir) on ansi2knr.  That directory is wanted for the
# Makefiles in subdirectories, but here we must omit it so automake gives
# the actual ansi2knr build rule, not "cd $(top_builddir) && make ansi2knr".
#
# AUTOMAKE_OPTIONS = 1.8 gnu no-dependencies


# Libtool -version-info for libgmp.la and libmp.la.  See "Versioning" in the
# libtool manual.
#
#	CURRENT:REVISION:AGE
#
# 1. No interfaces changed, only implementations (good): Increment REVISION.
#
# 2. Interfaces added, none removed (good): Increment CURRENT, increment
#    AGE, set REVISION to 0.
#
# 3. Interfaces removed (BAD, breaks upward compatibility): Increment
#    CURRENT, set AGE and REVISION to 0.
#
# Do this separately for libgmp, libgmpxx and libmp, and only for releases.
#
#	  GMP	   -version-info
#       release   libgmp  libgmpxx libmp
#        2.0.x      -        -       -
#        3.0      3:0:0      -     3:0:0
#        3.0.1    3:1:0      -     3:0:0
#        3.1      4:0:1      -     4:0:1
#        3.1.1    4:1:1      -     4:1:1
#        4.0      5:0:2    3:0:0   4:2:1
#        4.0.1    5:1:2    3:1:0   4:3:1
#        4.1      6:0:3    3:2:0   4:4:1
#        4.1.1    6:1:3    3:3:0   4:5:1
#        4.1.2    6:2:3    3:4:0   4:6:1
#        4.1.3    6:3:3    3:5:0   4:7:1
#        4.1.4    6:3:3    3:5:0   4:7:1	WRONG, same as 4.1.3!
#        4.2      6:0:3    3:2:0   4:4:1	REALLY WRONG, same as 4.1!
#        4.2.1    7:1:4    4:1:1   4:10:1	WRONG for libgmpxx
#        4.2.2    7:2:4    4:2:0   4:11:1
#        4.2.3    7:3:4    4:3:0   4:12:1
#        4.2.4    7:4:4    4:4:0   4:13:1
#        4.3.0    8:0:5    5:0:1   4:14:1
#        4.3.1    8:1:5    5:1:1   4:15:1	WRONG Really used same as 4.3.0
#        4.3.2    8:2:5    5:2:1   4:16:1
#        5.0.0    9:0:6    6:0:2   4:20:1	Should have been 10:0:0
#        5.0.1   10:1:0    6:1:2   4:21:1
#        5.0.2   10:2:0    6:2:2   4:22:1
#        5.0.3   10:3:0    6:3:2   4:23:1
#        5.0.4   10:4:0    6:4:2   4:24:1
#        5.0.5   10:5:0    6:5:2   4:25:1
#        5.1.0   11:0:1    7:0:3     -
#        5.1.1   11:1:1    7:1:3     -
#        5.1.2   11:2:1    7:2:3     -
#        6.0.0   12:0:2    8:0:4     -
#        6.1.0   13:0:3    9:0:5     -
#        6.1.1   13:1:3    9:1:5     -
#        6.1.2   13:2:3    9:2:5     -
#
# Starting at 3:0:0 is a slight abuse of the versioning system, but it
# ensures we're past soname libgmp.so.2, which was used on Debian GNU/Linux
# packages of gmp 2.  Pretend gmp 2 was 2:0:0, so the interface changes for
# gmp 3 mean 3:0:0 is right.
#
# We interpret "implementation changed" in item "1." above as meaning any
# release, ie. the REVISION is incremented every time (if nothing else).
# Even if we thought the code generated will be identical on all systems,
# it's still good to get the shared library filename (like
# libgmpxx.so.3.0.4) incrementing, to make it clear which GMP it's from.

SO_VERSION = 13:2:3
#LIBGMP_LT_CURRENT    = 13
#LIBGMP_LT_REVISION   = 2
#LIBGMP_LT_AGE        = 3

SO_CXX_VERSION = 9:2:5
#LIBGMPXX_LT_CURRENT  = 9
#LIBGMPXX_LT_REVISION = 2
#LIBGMPXX_LT_AGE      = 5

SUBDIRS = mpn mpz mpq mpf printf scanf rand cxx tune # tests demos doc

EXTRA_DIST = configfsf.guess configfsf.sub .gdbinit INSTALL.autoconf \
	     COPYING.LESSERv3 COPYINGv2 COPYINGv3


if WANT_CXX
GMPXX_HEADERS_OPTION = gmpxx.h
endif
EXTRA_DIST += gmpxx.h

# gmp.h and mp.h are architecture dependent, mainly since they encode the
# limb size used in libgmp.  For that reason they belong under $exec_prefix
# not $prefix, strictly speaking.
#
# $exec_prefix/include is not in the default include path for gcc built to
# the same $prefix and $exec_prefix, which might mean gmp.h is not found,
# but anyone knowledgeable enough to be playing with exec_prefix will be able
# to address that.
#
includeexecdir = $(exec_prefix)/include
include_HEADERS = $(GMPXX_HEADERS_OPTION)
nodist_includeexec_HEADERS = gmp.h
lib_LIBRARIES = libgmp.a $(GMPXX_LIBRARIES_OPTION)

BUILT_SOURCES = gmp.h

DISTCLEANFILES = $(BUILT_SOURCES) config.m4 @gmp_srclinks@

# Tell gmp.h it's building gmp, not an application, used by windows DLL stuff.
AM_CPPFLAGS=-D__GMP_WITHIN_GMP

MPF_OBJECTS = mpf/init$U.o mpf/init2$U.o mpf/inits$U.o mpf/set$U.o	    \
  mpf/set_ui$U.o mpf/set_si$U.o mpf/set_str$U.o mpf/set_d$U.o	    \
  mpf/set_z$U.o mpf/iset$U.o mpf/iset_ui$U.o mpf/iset_si$U.o	    \
  mpf/iset_str$U.o mpf/iset_d$U.o mpf/clear$U.o mpf/clears$U.o	    \
  mpf/get_str$U.o mpf/dump$U.o mpf/size$U.o mpf/eq$U.o mpf/reldiff$U.o \
  mpf/sqrt$U.o mpf/random2$U.o mpf/inp_str$U.o mpf/out_str$U.o	    \
  mpf/add$U.o mpf/add_ui$U.o mpf/sub$U.o mpf/sub_ui$U.o mpf/ui_sub$U.o \
  mpf/mul$U.o mpf/mul_ui$U.o mpf/div$U.o mpf/div_ui$U.o mpf/cmp_z$U.o  \
  mpf/cmp$U.o mpf/cmp_d$U.o mpf/cmp_ui$U.o mpf/cmp_si$U.o		    \
  mpf/mul_2exp$U.o mpf/div_2exp$U.o mpf/abs$U.o mpf/neg$U.o		    \
  mpf/set_q$U.o mpf/get_d$U.o mpf/get_d_2exp$U.o mpf/set_dfl_prec$U.o   \
  mpf/set_prc$U.o mpf/set_prc_raw$U.o mpf/get_dfl_prec$U.o               \
  mpf/get_prc$U.o mpf/ui_div$U.o mpf/sqrt_ui$U.o                         \
  mpf/ceilfloor$U.o mpf/trunc$U.o mpf/pow_ui$U.o			    \
  mpf/urandomb$U.o mpf/swap$U.o					    \
  mpf/fits_sint$U.o mpf/fits_slong$U.o mpf/fits_sshort$U.o		    \
  mpf/fits_uint$U.o mpf/fits_ulong$U.o mpf/fits_ushort$U.o		    \
  mpf/get_si$U.o mpf/get_ui$U.o					    \
  mpf/int_p$U.o

MPZ_OBJECTS = mpz/abs$U.o mpz/add$U.o mpz/add_ui$U.o			\
  mpz/aorsmul$U.o mpz/aorsmul_i$U.o mpz/and$U.o mpz/array_init$U.o	\
  mpz/bin_ui$U.o mpz/bin_uiui$U.o					\
  mpz/cdiv_q$U.o mpz/cdiv_q_ui$U.o					\
  mpz/cdiv_qr$U.o mpz/cdiv_qr_ui$U.o					\
  mpz/cdiv_r$U.o mpz/cdiv_r_ui$U.o mpz/cdiv_ui$U.o			\
  mpz/cfdiv_q_2exp$U.o mpz/cfdiv_r_2exp$U.o				\
  mpz/clear$U.o mpz/clears$U.o mpz/clrbit$U.o			\
  mpz/cmp$U.o mpz/cmp_d$U.o mpz/cmp_si$U.o mpz/cmp_ui$U.o		\
  mpz/cmpabs$U.o mpz/cmpabs_d$U.o mpz/cmpabs_ui$U.o			\
  mpz/com$U.o mpz/combit$U.o						\
  mpz/cong$U.o mpz/cong_2exp$U.o mpz/cong_ui$U.o			\
  mpz/divexact$U.o mpz/divegcd$U.o mpz/dive_ui$U.o			\
  mpz/divis$U.o mpz/divis_ui$U.o mpz/divis_2exp$U.o mpz/dump$U.o	\
  mpz/export$U.o mpz/mfac_uiui$U.o					\
  mpz/2fac_ui$U.o mpz/fac_ui$U.o mpz/oddfac_1$U.o mpz/prodlimbs$U.o	\
  mpz/fdiv_q_ui$U.o mpz/fdiv_qr$U.o mpz/fdiv_qr_ui$U.o		\
  mpz/fdiv_r$U.o mpz/fdiv_r_ui$U.o mpz/fdiv_q$U.o			\
  mpz/fdiv_ui$U.o mpz/fib_ui$U.o mpz/fib2_ui$U.o mpz/fits_sint$U.o	\
  mpz/fits_slong$U.o mpz/fits_sshort$U.o mpz/fits_uint$U.o		\
  mpz/fits_ulong$U.o mpz/fits_ushort$U.o mpz/gcd$U.o			\
  mpz/gcd_ui$U.o mpz/gcdext$U.o mpz/get_d$U.o mpz/get_d_2exp$U.o	\
  mpz/get_si$U.o mpz/get_str$U.o mpz/get_ui$U.o mpz/getlimbn$U.o	\
  mpz/hamdist$U.o							\
  mpz/import$U.o mpz/init$U.o mpz/init2$U.o mpz/inits$U.o		\
  mpz/inp_raw$U.o mpz/inp_str$U.o mpz/invert$U.o			\
  mpz/ior$U.o mpz/iset$U.o mpz/iset_d$U.o mpz/iset_si$U.o		\
  mpz/iset_str$U.o mpz/iset_ui$U.o mpz/jacobi$U.o mpz/kronsz$U.o	\
  mpz/kronuz$U.o mpz/kronzs$U.o mpz/kronzu$U.o			\
  mpz/lcm$U.o mpz/lcm_ui$U.o mpz/limbs_finish$U.o			\
  mpz/limbs_modify$U.o mpz/limbs_read$U.o mpz/limbs_write$U.o	\
  mpz/lucnum_ui$U.o mpz/lucnum2_ui$U.o				\
  mpz/millerrabin$U.o mpz/mod$U.o mpz/mul$U.o mpz/mul_2exp$U.o	\
  mpz/mul_si$U.o mpz/mul_ui$U.o					\
  mpz/n_pow_ui$U.o mpz/neg$U.o mpz/nextprime$U.o			\
  mpz/out_raw$U.o mpz/out_str$U.o mpz/perfpow$U.o mpz/perfsqr$U.o	\
  mpz/popcount$U.o mpz/pow_ui$U.o mpz/powm$U.o mpz/powm_sec$U.o	\
  mpz/powm_ui$U.o mpz/primorial_ui$U.o				\
  mpz/pprime_p$U.o mpz/random$U.o mpz/random2$U.o			\
  mpz/realloc$U.o mpz/realloc2$U.o mpz/remove$U.o mpz/roinit_n$U.o  \
  mpz/root$U.o mpz/rootrem$U.o mpz/rrandomb$U.o mpz/scan0$U.o	\
  mpz/scan1$U.o mpz/set$U.o mpz/set_d$U.o mpz/set_f$U.o		\
  mpz/set_q$U.o mpz/set_si$U.o mpz/set_str$U.o mpz/set_ui$U.o	\
  mpz/setbit$U.o							\
  mpz/size$U.o mpz/sizeinbase$U.o mpz/sqrt$U.o			\
  mpz/sqrtrem$U.o mpz/sub$U.o mpz/sub_ui$U.o mpz/swap$U.o		\
  mpz/tdiv_ui$U.o mpz/tdiv_q$U.o mpz/tdiv_q_2exp$U.o			\
  mpz/tdiv_q_ui$U.o mpz/tdiv_qr$U.o mpz/tdiv_qr_ui$U.o		\
  mpz/tdiv_r$U.o mpz/tdiv_r_2exp$U.o mpz/tdiv_r_ui$U.o		\
  mpz/tstbit$U.o mpz/ui_pow_ui$U.o mpz/ui_sub$U.o mpz/urandomb$U.o	\
  mpz/urandomm$U.o mpz/xor$U.o

MPQ_OBJECTS = mpq/abs$U.o mpq/aors$U.o				\
  mpq/canonicalize$U.o mpq/clear$U.o mpq/clears$U.o			\
  mpq/cmp$U.o mpq/cmp_si$U.o mpq/cmp_ui$U.o mpq/div$U.o		\
  mpq/get_d$U.o mpq/get_den$U.o mpq/get_num$U.o mpq/get_str$U.o	\
  mpq/init$U.o mpq/inits$U.o mpq/inp_str$U.o mpq/inv$U.o		\
  mpq/md_2exp$U.o mpq/mul$U.o mpq/neg$U.o mpq/out_str$U.o		\
  mpq/set$U.o mpq/set_den$U.o mpq/set_num$U.o			\
  mpq/set_si$U.o mpq/set_str$U.o mpq/set_ui$U.o			\
  mpq/equal$U.o mpq/set_z$U.o mpq/set_d$U.o				\
  mpq/set_f$U.o mpq/swap$U.o

MPN_OBJECTS = mpn/fib_table$U.o mpn/mp_bases$U.o

PRINTF_OBJECTS =							\
  printf/asprintf$U.o printf/asprntffuns$U.o				\
  printf/doprnt$U.o printf/doprntf$U.o printf/doprnti$U.o		\
  printf/fprintf$U.o							\
  printf/obprintf$U.o printf/obvprintf$U.o printf/obprntffuns$U.o	\
  printf/printf$U.o printf/printffuns$U.o				\
  printf/snprintf$U.o printf/snprntffuns$U.o				\
  printf/sprintf$U.o printf/sprintffuns$U.o				\
  printf/vasprintf$U.o printf/vfprintf$U.o printf/vprintf$U.o	\
  printf/vsnprintf$U.o printf/vsprintf$U.o				\
  printf/repl-vsnprintf$U.o

SCANF_OBJECTS =							\
  scanf/doscan$U.o scanf/fscanf$U.o scanf/fscanffuns$U.o	\
  scanf/scanf$U.o scanf/sscanf$U.o scanf/sscanffuns$U.o	\
  scanf/vfscanf$U.o scanf/vscanf$U.o scanf/vsscanf$U.o

RANDOM_OBJECTS =							\
  rand/rand$U.o rand/randclr$U.o rand/randdef$U.o rand/randiset$U.o	\
  rand/randlc2s$U.o rand/randlc2x$U.o rand/randmt$U.o		\
  rand/randmts$U.o rand/rands$U.o rand/randsd$U.o rand/randsdui$U.o	\
  rand/randbui$U.o rand/randmui$U.o

# no $U for C++ files
CXX_OBJECTS =								\
  cxx/isfuns.o cxx/ismpf.o cxx/ismpq.o cxx/ismpz.o cxx/ismpznw.o	\
  cxx/limits.o cxx/osdoprnti.o cxx/osfuns.o				\
  cxx/osmpf.o cxx/osmpq.o cxx/osmpz.o

# In libtool 1.5 it doesn't work to build libgmp.la from the convenience
# libraries like mpz/libmpz.la.  Or rather it works, but it ends up putting
# PIC objects into libgmp.a if shared and static are both built.  (The PIC
# objects go into mpz/.libs/libmpz.a, and thence into .libs/libgmp.a.)
#
# For now the big lists of objects above are used.  Something like mpz/*.lo
# would probably work, but might risk missing something out or getting
# something extra.  The source files for each .lo are listed in the
# Makefile.am's in the subdirectories.
#
# Currently, for libgmp, unlike libmp below, we're not using
# -export-symbols, since the tune and speed programs, and perhaps some of
# the test programs, want to access undocumented symbols.

libgmp_a_SOURCES = gmp-impl.h longlong.h				\
  assert.c compat.c errno.c extract-dbl.c invalid.c memory.c		\
  mp_bpl.c mp_clz_tab.c mp_dv_tab.c mp_minv_tab.c mp_get_fns.c mp_set_fns.c \
  version.c nextprime.c primesieve.c
EXTRA_libgmp_a_SOURCES = tal-debug.c tal-notreent.c tal-reent.c
libgmp_a_DEPENDENCIES = @TAL_OBJECT@		\
  $(MPF_OBJECTS) $(MPZ_OBJECTS) $(MPQ_OBJECTS)	\
  $(MPN_OBJECTS) @mpn_objs_in_libgmp@		\
  $(PRINTF_OBJECTS)  $(SCANF_OBJECTS) $(RANDOM_OBJECTS)
libgmp_a_LIBADD = $(libgmp_a_DEPENDENCIES)
libgmp_a_LDFLAGS = $(GMP_LDFLAGS) $(LIBGMP_LDFLAGS) \
  -version-info $(SO_VERSION)


# We need at least one .cc file in $(libgmpxx_la_SOURCES) so automake will
# use $(CXXLINK) rather than the plain C $(LINK).  cxx/dummy.cc is that
# file.

if WANT_CXX
GMPXX_LIBRARIES_OPTION = libgmpxx.a
endif
libgmpxx_a_SOURCES = cxx/dummy.cc
libgmpxx_a_DEPENDENCIES = $(CXX_OBJECTS) libgmp.la
libgmpxx_a_LIBADD = $(libgmpxx_a_DEPENDENCIES)
libgmpxx_a_LDFLAGS = $(GMP_LDFLAGS) $(LIBGMPXX_LDFLAGS) \
  -version-info $(SO_CXX_VERSION)



install-data-hook:
	@echo ''
	@echo '+-------------------------------------------------------------+'
	@echo '| CAUTION:                                                    |'
	@echo '|                                                             |'
	@echo '| If you have not already run "make check", then we strongly  |'
	@echo '| recommend you do so.                                        |'
	@echo '|                                                             |'
	@echo '| GMP has been carefully tested by its authors, but compilers |'
	@echo '| are all too often released with serious bugs.  GMP tends to |'
	@echo '| explore interesting corners in compilers and has hit bugs   |'
	@echo '| on quite a few occasions.                                   |'
	@echo '|                                                             |'
	@echo '+-------------------------------------------------------------+'
	@echo ''


# The "test -f" support for srcdir!=builddir is similar to the automake .c.o
# etc rules, but with each foo.c explicitly, since $< is not portable
# outside an inference rule.
#
# A quoted 'foo.c' is used with the "test -f"'s to avoid Sun make rewriting
# it as part of its VPATH support.  See the autoconf manual "Limitations of
# Make".
#
# Generated .h files which are used by gmp-impl.h are BUILT_SOURCES since
# they must exist before anything can be compiled.
#
# Other generated .h files are also BUILT_SOURCES so as to get all the
# build-system stuff over and done with at the start.  Also, dependencies on
# the .h files are not properly expressed for the various objects that use
# them.

EXTRA_DIST += bootstrap.c

fac_table.h: gen-fac$(EXEEXT_FOR_BUILD)
	./gen-fac $(GMP_LIMB_BITS) $(GMP_NAIL_BITS) >fac_table.h || (rm -f fac_table.h; exit 1)
BUILT_SOURCES += fac_table.h

gen-fac$(EXEEXT_FOR_BUILD): gen-fac$(U_FOR_BUILD).c bootstrap.c
	$(CC_FOR_BUILD) `test -f 'gen-fac$(U_FOR_BUILD).c' || echo '$(srcdir)/'`gen-fac$(U_FOR_BUILD).c -o gen-fac$(EXEEXT_FOR_BUILD)
DISTCLEANFILES += gen-fac$(EXEEXT_FOR_BUILD)
EXTRA_DIST += gen-fac.c


fib_table.h: gen-fib$(EXEEXT_FOR_BUILD)
	./gen-fib header $(GMP_LIMB_BITS) $(GMP_NAIL_BITS) >fib_table.h || (rm -f fib_table.h; exit 1)
BUILT_SOURCES += fib_table.h

mpn/fib_table.c: gen-fib$(EXEEXT_FOR_BUILD)
	./gen-fib table $(GMP_LIMB_BITS) $(GMP_NAIL_BITS) >mpn/fib_table.c || (rm -f mpn/fib_table.c; exit 1)
BUILT_SOURCES += mpn/fib_table.c

gen-fib$(EXEEXT_FOR_BUILD): gen-fib$(U_FOR_BUILD).c bootstrap.c
	$(CC_FOR_BUILD) `test -f 'gen-fib$(U_FOR_BUILD).c' || echo '$(srcdir)/'`gen-fib$(U_FOR_BUILD).c -o gen-fib$(EXEEXT_FOR_BUILD)
DISTCLEANFILES += gen-fib$(EXEEXT_FOR_BUILD)
EXTRA_DIST += gen-fib.c


mp_bases.h: gen-bases$(EXEEXT_FOR_BUILD)
	./gen-bases header $(GMP_LIMB_BITS) $(GMP_NAIL_BITS) >mp_bases.h || (rm -f mp_bases.h; exit 1)
BUILT_SOURCES += mp_bases.h

mpn/mp_bases.c: gen-bases$(EXEEXT_FOR_BUILD)
	./gen-bases table $(GMP_LIMB_BITS) $(GMP_NAIL_BITS) >mpn/mp_bases.c || (rm -f mpn/mp_bases.c; exit 1)
BUILT_SOURCES += mpn/mp_bases.c

gen-bases$(EXEEXT_FOR_BUILD): gen-bases$(U_FOR_BUILD).c bootstrap.c
	$(CC_FOR_BUILD) `test -f 'gen-bases$(U_FOR_BUILD).c' || echo '$(srcdir)/'`gen-bases$(U_FOR_BUILD).c -o gen-bases$(EXEEXT_FOR_BUILD) $(LIBM_FOR_BUILD)
DISTCLEANFILES += gen-bases$(EXEEXT_FOR_BUILD)
EXTRA_DIST += gen-bases.c


trialdivtab.h: gen-trialdivtab$(EXEEXT_FOR_BUILD)
	./gen-trialdivtab $(GMP_LIMB_BITS) 8000 >trialdivtab.h || (rm -f trialdivtab.h; exit 1)
BUILT_SOURCES += trialdivtab.h

gen-trialdivtab$(EXEEXT_FOR_BUILD): gen-trialdivtab$(U_FOR_BUILD).c bootstrap.c
	$(CC_FOR_BUILD) `test -f 'gen-trialdivtab$(U_FOR_BUILD).c' || echo '$(srcdir)/'`gen-trialdivtab$(U_FOR_BUILD).c -o gen-trialdivtab$(EXEEXT_FOR_BUILD) $(LIBM_FOR_BUILD)
DISTCLEANFILES += gen-trialdivtab$(EXEEXT_FOR_BUILD)
EXTRA_DIST += gen-trialdivtab.c


mpn/jacobitab.h: gen-jacobitab$(EXEEXT_FOR_BUILD)
	./gen-jacobitab >mpn/jacobitab.h || (rm -f mpn/jacobitab.h; exit 1)
BUILT_SOURCES += mpn/jacobitab.h

gen-jacobitab$(EXEEXT_FOR_BUILD): gen-jacobitab$(U_FOR_BUILD).c
	$(CC_FOR_BUILD) `test -f 'gen-jacobitab$(U_FOR_BUILD).c' || echo '$(srcdir)/'`gen-jacobitab$(U_FOR_BUILD).c -o gen-jacobitab$(EXEEXT_FOR_BUILD)
DISTCLEANFILES += gen-jacobitab$(EXEEXT_FOR_BUILD)
EXTRA_DIST += gen-jacobitab.c


mpn/perfsqr.h: gen-psqr$(EXEEXT_FOR_BUILD)
	./gen-psqr $(GMP_LIMB_BITS) $(GMP_NAIL_BITS) >mpn/perfsqr.h || (rm -f mpn/perfsqr.h; exit 1)
BUILT_SOURCES += mpn/perfsqr.h

gen-psqr$(EXEEXT_FOR_BUILD): gen-psqr$(U_FOR_BUILD).c bootstrap.c
	$(CC_FOR_BUILD) `test -f 'gen-psqr$(U_FOR_BUILD).c' || echo '$(srcdir)/'`gen-psqr$(U_FOR_BUILD).c -o gen-psqr$(EXEEXT_FOR_BUILD) $(LIBM_FOR_BUILD)
DISTCLEANFILES += gen-psqr$(EXEEXT_FOR_BUILD)
EXTRA_DIST += gen-psqr.c

# Distribute mini-gmp. Test sources copied by dist-hook.
EXTRA_DIST += mini-gmp/README mini-gmp/mini-gmp.c mini-gmp/mini-gmp.h \
	      mini-gmp/tests/Makefile mini-gmp/tests/run-tests

# Avoid: CVS - cvs directories
#        *~  - emacs backups
#        .#* - cvs merge originals
#
# *~ and .#* only occur when a whole directory without it's own Makefile.am
# is distributed, like "doc" or the mpn cpu subdirectories.
#
dist-hook:
	-find $(distdir) \( -name CVS -type d \) -o -name "*~" -o -name ".#*" \
		| xargs rm -rf
	cp "$(srcdir)"/mini-gmp/tests/*.[ch] "$(distdir)/mini-gmp/tests"
#	grep -F $(VERSION) $(srcdir)/Makefile.am \
#		| grep -q "^# *$(VERSION) *$(LIBGMP_LT_CURRENT):$(LIBGMP_LT_REVISION):$(LIBGMP_LT_AGE) *$(LIBGMPXX_LT_CURRENT):$(LIBGMPXX_LT_REVISION):$(LIBGMPXX_LT_AGE)"
#	test -z "`sed -n 's/^# *[0-9]*\.[0-9]*\.[0-9]* *\([0-9]*:[0-9]*:[0-9]*\) *\([0-9]*:[0-9]*:[0-9]*\) *\([0-9]*:[0-9]*:[0-9]*\).*/A\1\nB\2\nC\3/p' $(srcdir)/Makefile.am | grep -v 'A6:3:3\|B3:5:0\|C4:7:1' | sort | uniq -d`"

.PHONY: check-mini-gmp clean-mini-gmp

check-mini-gmp:
	abs_srcdir="`cd $(srcdir) && pwd`" ; \
	$(MKDIR_P) mini-gmp/tests \
	&& cd mini-gmp/tests \
	&& TEST_LIBRARY_PATH="../../.libs"  \
	   $(MAKE) -f "$$abs_srcdir/mini-gmp/tests/Makefile" \
		VPATH="$$abs_srcdir/mini-gmp/tests" \
		srcdir="$$abs_srcdir/mini-gmp/tests" \
		MINI_GMP_DIR="$$abs_srcdir/mini-gmp" \
		LDFLAGS="-L../../.libs" \
		LIBS="-lgmp -lm" \
		CC="$(CC)" CFLAGS="$(CFLAGS)" CPPFLAGS="-I../.." check

clean-mini-gmp:
	if [ -d mini-gmp/tests ] ; then \
	  abs_srcdir="`cd $(srcdir) && pwd`" ; \
	  cd mini-gmp/tests \
	  && $(MAKE) -f "$$abs_srcdir/mini-gmp/tests/Makefile" clean ; \
	fi

clean-local: clean-mini-gmp
distclean-local: clean-mini-gmp
