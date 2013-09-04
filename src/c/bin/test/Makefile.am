AM_CPPFLAGS = $(PACKAGE_CPPFLAGS) -I$(top_srcdir)/src/c/include

bin_PROGRAMS = hello

hello_SOURCES = \
	hello.c \
	hello.h

hello_LDADD = \
	$(top_builddir)/src/c/lib/test/libmcsftest.la
