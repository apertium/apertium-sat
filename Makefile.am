###############################################################################
## Makefile for apertium-sat
###############################################################################

LANG1=sat
BASENAME=apertium-$(LANG1)

TARGETS_COMMON =			\
	$(LANG1).automorf.bin		\
	$(LANG1).automorf.att.gz	\
	$(LANG1).autogen.bin		\
	$(LANG1).autogen.att.gz		\
	$(LANG1).autopgen.bin		\
	$(LANG1).rlx.bin

# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Santali transducer
###############################################################################

$(LANG1).autogen.bin: $(BASENAME).$(LANG1).dix .deps/.d
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(LANG1).automorf.bin: $(BASENAME).$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@ $(srcdir)/$(BASENAME).$(LANG1).acx

$(LANG1).autogen.att.gz: $(LANG1).autogen.bin
	lt-print $< | gzip -9 -c -n > $@

$(LANG1).automorf.att.gz: $(LANG1).automorf.bin
	lt-print $< | gzip -9 -c -n > $@

$(LANG1).autopgen.bin: $(BASENAME).post-$(LANG1).dix
	lt-comp lr $< $@

###############################################################################
## Disambiguation rules
###############################################################################

$(LANG1).rlx.bin: $(BASENAME).$(LANG1).rlx
	cg-comp $< $@

###############################################################################
## Unigram tagger
###############################################################################

#$(LANG1).prob: corpus/$(LANG1).tagged
#	apertium-tagger -s 0 -u 2 $@ $<

###############################################################################
## Distribution
###############################################################################
EXTRA_DIST=$(BASENAME).$(LANG1).dix		\
		$(BASENAME).$(LANG1).acx	\
		$(BASENAME).$(LANG1).rlx	\
		$(BASENAME).post-$(LANG1).dix	\
		$(LANG1).prob			\
		modes.xml

###############################################################################
## Installation stuff
###############################################################################
#
#   apertium_sat_dir: This is where the compiled binaries go
#   apertium_sat_srcdir: This is where the source files go

apertium_satdir=$(prefix)/share/apertium/$(BASENAME)/
apertium_sat_srcdir=$(prefix)/share/apertium/$(BASENAME)/

apertium_sat_DATA=$(TARGETS_COMMON) \
	$(LANG1).prob \
	$(BASENAME).$(LANG1).dix \
	$(BASENAME).$(LANG1).rlx \
	$(BASENAME).post-$(LANG1).dix

pkgconfigdir = $(prefix)/share/pkgconfig
pkgconfig_DATA = $(BASENAME).pc

noinst_DATA=modes/$(LANG1)-morph.mode

install-data-local: install-modes
uninstall-local: uninstall-modes

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	apertium-regtest test
