ACLOCAL_AMFLAGS = -I m4

AM_DISTCHECK_CONFIGURE_FLAGS = \
	HAREFLAGS="$(HAREFLAGS)" \
	$(HARE_ENV)

HARE_MOD = $(srcdir)/`for f in $($(@)_SOURCES);do dirname $$f;done|sort|sed q`

HARE_ENV = \
	HAREPATH="$(HAREPATH)" \
	HAREC="$(HAREC)" \
	QBE="$(QBE)" \
	AR="$(AR)" \
	ARFLAGS="$(ARFLAGS)" \
	AS="$(AS)" \
	ASFLAGS="$(ASFLAGS)" \
	LD="$(LD)" \
	LDLINKFLAGS="$(LDLINKFLAGS)"

HARE_BUILD = env $(HARE_ENV) $(HARE) build -t $(host_cpu)

# Hijack the libtool-based C build system instead of passing hare flags
# via the environment. This composes better with per-program flags. We
# can't build both Hare and C programs with the same makefile, but this
# is still possible in the same automake project.
CFLAGS = $(HAREFLAGS)
LDFLAGS =
LIBS =
CCLD = $(HARE_BUILD)

bin_PROGRAMS = haredoc

haredoc_SOURCES = \
	cmd/haredoc/color.ha \
	cmd/haredoc/docstr.ha \
	cmd/haredoc/env.ha \
	cmd/haredoc/errors.ha \
	cmd/haredoc/hare.ha \
	cmd/haredoc/html.ha \
	cmd/haredoc/main.ha \
	cmd/haredoc/resolver.ha \
	cmd/haredoc/sort.ha \
	cmd/haredoc/tty.ha \
	cmd/haredoc/util.ha

haredoc_DEPENDENCIES = $(haredoc_SOURCES)

haredoc_LDADD = $(HARE_MOD)

haredoc_CFLAGS = -D HAREPATH:str="\"$(HAREPATH)\""

SUFFIXES = .scd

.scd.1 .scd.2 .scd.3 .scd.4 .scd.5 .scd.6 .scd.7 .scd.8 .scd.9:
	@mkdir -p `dirname $@`
	$(AM_V_GEN)$(SCDOC) <$< >$@ || rm -f $@

dist_man1_MANS = cmd/haredoc/haredoc.1

CLEANFILES = $(dist_man1_MANS)
EXTRA_DIST = $(dist_man1_MANS:.1=.scd)
