# Process this file with automake to create Makefile.in

bundledir = $(BUNDLEDIR)/opensc
enginedir = $(libdir)/openssl

MAINTAINERCLEANFILES = Makefile.in

EXTRA_DIST = Makefile.mak engine_pkcs11.def 

engine_LTLIBRARIES = engine_pkcs11.la

OPENSSL_CFLAGS = \
	-DOPENSSL_THREADS -D_REENTRANT -DDSO_DLFCN -DHAVE_DLFCN_H \
	-DOPENSSL_NO_KRB5 -DL_ENDIAN -DTERMIO -DENGINE_DYNAMIC_SUPPORT \
	-DSHA1_ASM -DMD5_ASM -DRMD160_ASM

engine_pkcs11_la_SOURCES = \
	hw_pkcs11.c engine_pkcs11.c engine_pkcs11.h 
engine_pkcs11_la_CFLAGS = $(OPENSSL_CFLAGS) $(LIBP11_CFLAGS) -I$(srcdir)/../libp11 
engine_pkcs11_la_LIBADD = $(ENGINE_LINK) $(OPENSSL_LIBS) $(LIBP11_LIBS)
engine_pkcs11_la_LDFLAGS = -module -avoid-version

install-exec-local: install-engineLTLIBRARIES
if HAVE_BUNDLES
	-${top_srcdir}/libtool-bundle $(DESTDIR)$(enginedir)/engine_pkcs11.so \
		$(DESTDIR)$(bundledir)/
endif

uninstall-local: uninstall-engineLTLIBRARIES
if HAVE_BUNDLES
	rm -rf $(DESTDIR)$(bundledir)/engine_pkcs11.bundle/
endif