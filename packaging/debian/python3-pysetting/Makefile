PROJECT ?= python3-pysetting
PREFIX ?= /usr
BINDIR ?= $(PREFIX)/bin
LIBDIR ?= $(PREFIX)/lib
MANDIR ?= $(PREFIX)/share/man
ETCDIR ?= /etc
VERSION=0.0.7

.PHONY: all
all: build

.PHONY: build
build: 
	./build.sh

#
# Test
#
.PHONY: test
test:

#
# Clean
#
.PHONY: distclean
distclean: clean

.PHONY: clean
clean: clean-deb


.PHONY: clean-deb
clean-deb:
	rm -rf debian/.debhelper debian/python3-pysetting/ debian/debhelper-build-stamp debian/files debian/*.debhelper.log debian/*.postrm.debhelper debian/*.substvars

#
# Release
#
.PHONY: dch
dch: debian/changelog
	update-changelog.sh

.PHONY: deb
deb: debian
	debuild --no-lintian --lintian-hook "lintian --fail-on error,warning --suppress-tags bad-distribution-in-changes-file -- %p_%v_*.changes" --no-sign -b

.PHONY: release
release:
	gh workflow run .github/workflows/new_version.yml
