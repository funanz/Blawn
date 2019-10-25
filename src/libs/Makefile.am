bin_SCRIPTS = cridge

EXTRA_DIST = builtins.c
CLEANFILES = builtins.o builtins.bridge

builtins.o: builtins.c
	$(CLANG) -c $(CFLAGS) -o $@ $<

builtins.bridge: builtins.c
	./cridge $<

all-local: builtins.o builtins.bridge

install-data-local:
	$(MKDIR_P) $(DESTDIR)$(pkglibdir)
	$(INSTALL_DATA) builtins.o $(DESTDIR)$(pkglibdir)
	$(INSTALL_DATA) builtins.bridge $(DESTDIR)$(pkglibdir)

uninstall-local:
	$(RM) $(DESTDIR)$(pkglibdir)/builtins.o
	$(RM) $(DESTDIR)$(pkglibdir)/builtins.bridge
