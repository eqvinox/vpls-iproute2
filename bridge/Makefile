BROBJ = bridge.o fdb.o monitor.o link.o mdb.o vlan.o

include ../Config

ifeq ($(IP_CONFIG_SETNS),y)
	CFLAGS += -DHAVE_SETNS
endif

ifeq ($(HAVE_ELF),y)
	CFLAGS += -DHAVE_ELF
	LDLIBS += -lelf
endif
ifeq ($(HAVE_MNL),y)
	CFLAGS += -DHAVE_LIBMNL $(shell $(PKG_CONFIG) libmnl --cflags)
	LDLIBS += $(shell $(PKG_CONFIG) libmnl --libs)
endif

all: bridge

bridge: $(BROBJ) $(LIBNETLINK)
	$(QUIET_LINK)$(CC) $^ $(LDFLAGS) $(LDLIBS) -o $@

install: all
	install -m 0755 bridge $(DESTDIR)$(SBINDIR)

clean:
	rm -f $(BROBJ) bridge
