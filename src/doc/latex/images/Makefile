#fig2dev Version 3.2 Patchlevel 1:
#FIG2EPS = fig2dev -L ps -c -m 0.5 -P -n $@

#fig2dev Version 3.2 Patchlevel 3c:
FIG2EPS = fig2dev -L eps
GIF2PNM = giftopnm
PNM2PS = pnmtops -noturn
PNG2PNM = pngtopnm
PS2EPSI = ps2epsi
PLOT2EPS = gnuplot
DOT2PNG = dot -Tpng
FIG_OBJ = $(subst .fig,.eps,$(wildcard *.fig))
GIF_OBJ = $(subst .gif,.eps,$(wildcard *.gif))
PNG_OBJ = $(subst .png,.eps,$(wildcard *.png))
PLOT_OBJ = $(subst .plot,.eps,$(wildcard *.plot))
DOT_OBJ = $(subst .dot,.eps,$(wildcard *.dot))

all: $(FIG_OBJ) $(GIF_OBJ) $(PNG_OBJ) $(PLOT_OBJ) $(DOT_OBJ)

%.eps: %.dot
	$(DOT2PNG) -v $< | $(PNG2PNM) | $(PNM2PS) >$@

%.eps: %.png
	cat $< | $(PNG2PNM) | $(PNM2PS) >$@

%.eps: %.plot %.data
	$(PLOT2EPS) $<

%.eps: %.fig
	$(FIG2EPS) $< $@

%.eps: %.gif
	$(GIF2PNM) $< | $(PNM2PS) > $@

objclean:
	rm -f $(FIG_OBJ) $(GIF_OBJ) $(PLOT_OBJ)

bkpclean:
	rm -f *~ *.bak

clean: objclean

veryclean: objclean bkpclean
