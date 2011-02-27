SRCDIR  ?= $(dir $(realpath $(lastword $(MAKEFILE_LIST))))
VPATH   ?= $(SRCDIR)
XSLT    ?= xsltproc
INSTALL ?= install
SITE    ?= $(HOME)/Sites/silisec

IMAGES += Facebook_icon.png linkedin-button.png rss_icon2.png
IMAGES += Twitter_256x256.png linkedin_icon2.png twitter_icon2.png
IMAGES += facebook_icon2.png rss2007.gif

all: index.html atom.xml older.html

install: install-srcdir install-imgdir install-generated

index.html: index.xsl index.xml articles.xml
	$(XSLT) -o $@ --param articlesxml "'$(filter %articles.xml,$^)'" \
	  $< $(filter %index.xml,$^)

older.html: index.xsl index.xml older.xml
	$(XSLT) -o $@ --param articlesxml "'$(filter %older.xml,$^)'" \
	  $< $(filter %index.xml,$^)

atom.xml: atom.xsl articles.xml
	$(XSLT) -o $@ $< $(filter %articles.xml,$^)

install-imgdir: $(foreach img,$(IMAGES),img/$(img))
	$(INSTALL) -d -m 0755 $(SITE)
	$(INSTALL) -d -m 0755 $(SITE)/img
	$(INSTALL) -C -m 0644 $^ $(SITE)/img

install-srcdir: main.css error.html
	$(INSTALL) -d -m 0755 $(SITE)
	$(INSTALL) -C -m 0644 $^ $(SITE)

install-generated: index.html atom.xml older.html
	$(INSTALL) -d -m 0755 $(SITE)
	$(INSTALL) -C -m 0644 $^ $(SITE)

clean:
	rm -f index.html older.html atom.xml
