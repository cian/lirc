#
# Template for building a lirc userspace driver out of tree.
# Requires that lirc is installed in system locations, in
# particular that the /usr/lib[64]/pkgconfig/lirc-driver.pc
# is in place (/usr/local/lib/pkgconfig/... is also OK).
# The required file plugindocs.mk might live in a -doc
# package which then is needed.
#


driver          = irman_drv

all:  $(driver).so

CFLAGS          += $(shell pkg-config --cflags lirc-driver)
LDFLAGS         += $(shell pkg-config --libs lirc-driver)
PLUGINDIR       ?= $(shell pkg-config --variable=plugindir lirc-driver)
CONFIGDIR       ?= $(shell pkg-config --variable=configdir lirc-driver)
PLUGINDOCS      ?= $(shell pkg-config --variable=plugindocs lirc-driver)

include $(PLUGINDOCS)/plugindocs.mk

$(driver).o: $(driver).c

$(driver).so: $(driver).o
	gcc --shared -fpic $(LDFLAGS) -o $@ $<

install: $(driver).so
	install $< $(PLUGINDIR)
	install irman.conf $(CONFIGDIR)
	install irman.html $(PLUGINDOCS)
	$(MAKE) update

clean:
	rm -f *.o *.so
