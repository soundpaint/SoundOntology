PS_OBJ	=	$(wildcard images/*.ps)
EPS_OBJ	=	$(wildcard images/*.eps)
IMG_OBJ	=	$(PS_OBJ) $(EPS_OBJ)
OBJ	=	lac2006_ontology.ps lac2006_ontology.pdf

all: $(OBJ)

%.pdf: %.ps
	ps2pdf -sPAPERSIZE=a4 $< $@

%.ps: %.dvi
	dvips -o $@ $<

%.dvi: %.tex %.bib
	cd images ; make all # FIXME: replace this with proper rule
	latex $< # -src-specials=cr,display,hbox,math,par,parend,vbox $<
	-bibtex $*
	diff -q $*.bbl $*.bbllast || ( cp -p $*.bbl $*.bbllast ; rm $@ ; make $@ ) # fixpoint strategy: recompile until no further change arises
	diff -q $*.log $*.loglast || ( cp -p $*.log $*.loglast ; rm $@ ; make $@ ) # this works reasonable only if a make/latex run cycle takes pretty much less than a minute since the time (date, hour, minutes) is recorded in the log file

tocclean:
	rm -f *.toc *.toclast

bibclean:
	rm -f *.blg *.bbl *.bbllast resh.bib bu*.bib

texclean:
	rm -f *.log *.loglast *.aux *.dvi *.cb

objclean: bibclean tocclean texclean
	rm -f *.ps
	cd images ; make objclean

bkpclean:
	rm -f *~ *.bak
	cd images ; make bkpclean

clean: objclean

veryclean: objclean bkpclean
