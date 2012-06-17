#********************************************************
# Makefile for LaTeX documents
#
# Copyright 2009 by Didier Roche <didrocks@ubuntu.com>
#
# Provided under the terms of CC:BY-SA
#*******************************************************

DOC = main
#VERSION = $$(sed -n 's/\\ProvidesPackage{pagedegardeUAG}\[*\]}/\1/p' tex/latex/pagedegareUAG.sty | sed 's/ //g')
VERSION = `grep ProvidesPackage uag_style/pagedegardeUAG.sty | cut -d "[" -f2 | cut -d " " -f1 | sed 's./.-.g'`
COMPIL = pdflatex # put latex or pdflatex depending on what you prefer 

  #*  all : généralement la première du fichier, elle regroupe dans ces dépendances l'ensemble des exécutables à produire.
  #* clean : elle permet de supprimer tout les fichiers intermédiaires.
  #* mrproper : elle supprime tout ce qui peut être régénéré et permet une reconstruction complète du projet.


all : $(DOC).pdf
.PHONY: all install clean mrproper

$(DOC).pdf: $(DOC).tex
	while ( \
	$(COMPIL) -interaction=nonstopmode $(DOC).tex || true ; \
	$(COMPIL) -interaction=nonstopmode $(DOC).tex || true ; \
	grep -q "get cross-references right" $(DOC).log ) do true ; \
	done
	if [ "$(COMPIL)" = "latex " ] ; then \
		dvips  $(DOC).dvi ; \
		ps2pdf $(DOC).ps  ; \
	fi


clean:
	for i in "." "*" "*/*" ; do   \
		rm -rf $$i/*~       ; \
		rm -rf $$i/*.backup ; \
		rm -rf $$i/*.aux    ; \
	        rm -rf $$i/*.bbl    ; \
	        rm -rf $$i/*.blg    ; \
	    rm -rf $$i/*.glo        ; \
		rm -rf $$i/*.gls    ; \
	    rm -rf $$i/*.idx        ; \
		rm -rf $$i/*.ilg    ; \
	    rm -rf $$i/*.ind        ; \
		rm -rf $$i/*.lof    ; \
	    rm -rf $$i/*.log        ; \
		rm -rf $$i/*.lot    ; \
	    rm -rf $$i/*.out        ; \
		rm -rf $$i/*.toc    ; \
	    rm -rf $$i/*.som        ; \
	done ;
	rm -rf $(DOC).dvi $(DOC).ps

mrproper: clean
	rm -rf $(DOC).pdf

install: $(DOC).pdf
	cp $(DOC).pdf ./page-de-garde-UAG-$(VERSION).pdf
