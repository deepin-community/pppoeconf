DOMAIN=pppoeconf
POFILES=$(wildcard *.po)
MOFILES=$(patsubst %.po,%.mo,$(POFILES))
LINGUAS=$(basename $(POFILES))
MAINDIR=..
GETTEXTFILES=$(MAINDIR)/pppoeconf
POTFILE=$(DOMAIN).pot
DESTDIR=/

%.mo: %.po
	msgfmt --statistics -o $@ $<

%.po: $(DOMAIN).pot
	msgmerge -U $*.po $(DOMAIN).pot

$(DOMAIN).pot: $(GETTEXTFILES)
	$(shell xgettext -L Shell -o $(DOMAIN).pot $(GETTEXTFILES))

update-po:
	-for lang in $(LINGUAS); do\
	    msgmerge -U $$lang.po $(DOMAIN).pot; \
	done

install: $(MOFILES)
	-for lang in $(LINGUAS); do\
	    install -d $(DESTDIR)/usr/share/locale/$$lang/LC_MESSAGES/; \
	    install -m 644 $$lang.mo $(DESTDIR)/usr/share/locale/$$lang/LC_MESSAGES/$(DOMAIN).mo; \
	done

all: update-po $(MOFILES)

clean:
	- rm *.mo *~

.PHONY: update-po
