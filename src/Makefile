#
# Makefile	Makefile for bootlogd
#		Targets:   all      compiles everything
#		           install  installs the binaries (not the scripts)
#                          clean    cleans up object files
#			   clobber  really cleans up
#
# Version:	@(#)Makefile  2.85-13  23-Mar-2004  miquels@cistron.nl
#

# Version from sysvinit this was based on, 2.95.
# And an additional monotonically increasing number.
VERSION = "2.95.2"

CPPFLAGS =
CFLAGS  ?= -O2 -Werror
override CFLAGS += -ansi -fomit-frame-pointer -fstack-protector-strong -W -Wall -Wunreachable-code -Wformat -Werror=format-security -D_XOPEN_SOURCE -D_GNU_SOURCE -DVERSION=\"$(VERSION)\"
override CFLAGS += $(shell getconf LFS_CFLAGS)
STATIC	=
MANDB	:= s@^\('\\\\\"\)[^\*-]*-\*- coding: [^[:blank:]]\+ -\*-@\1@

BIN	= bootlogd

MAN8	= bootlogd.8

INSTALL_EXEC	= install -m 755
INSTALL_DATA	= install -m 644
INSTALL_DIR	= install -m 755 -d
MANDIR		= /share/man

all:		$(BIN)

bootlogd:	LDLIBS += -lutil $(STATIC)
bootlogd:	bootlogd.o

bootlogd.o:	bootlogd.c

# ----

cleanobjs:
		rm -f *.o

clean:		cleanobjs
		@echo Type \"make clobber\" to really clean up.

clobber:	cleanobjs
		rm -f $(BIN)

distclean:	clobber

install:	all
		$(INSTALL_DIR) $(PREFIX)/bin/
		for i in $(BIN); do \
			$(INSTALL_EXEC) $$i $(PREFIX)/bin/ ; \
		done
		$(INSTALL_DIR) $(PREFIX)$(MANDIR)/man8/
		for man in $(MAN8); do \
			$(INSTALL_DATA) ../man/$$man $(PREFIX)$(MANDIR)/man8/; \
			sed -i "1{ $(MANDB); }" $(PREFIX)$(MANDIR)/man8/$$man ; \
		done
