DOC = cheats_sheet
PDFLATEX = pdflatex -shell-escape -interaction=nonstopmode -file-line-error

all: $(DOC).pdf clean

$(DOC).pdf: $(DOC).tex
	$(PDFLATEX) $(DOC).tex

clean :
	rm -f $(DOC).log $(DOC).aux $(DOC).blg $(DOC).toc
