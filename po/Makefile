XGETTEXT = xgettext
MSGFMT = msgfmt
MSGMERGE = msgmerge

LOCALEDIR = /usr/share/locale

.SUFFIXES: .po .mo .pot

%.mo: %.po
	$(MSGFMT) -o $@ $<

PO = $(wildcard *.po)
LANG = $(basename $(PO))
MO = $(addsuffix .mo,$(LANG))
SOURCES = ../adduser ../deluser ../AdduserCommon.pm

all: update $(MO)
update: adduser.pot
	-@for po in $(PO); do \
	echo -n "Updating $$po"; \
	$(MSGMERGE) -U $$po adduser.pot; \
	done;

adduser.pot: $(SOURCES)
	$(XGETTEXT) -c -L Perl -kgtx \
	--msgid-bugs-address=adduser-devel@lists.alioth.debian.org \
	-o $@ $(SOURCES)

install: all
	for i in $(MO) ; do \
	  t=$(DESTDIR)/$(LOCALEDIR)/`basename $$i .mo`/LC_MESSAGES ;\
	  install -d $$t ;\
	  install -m 644 $$i $$t/adduser.mo ;\
	done

clean:
	$(RM) $(MO) *~

.PHONY: update
