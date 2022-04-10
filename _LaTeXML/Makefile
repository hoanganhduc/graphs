STATIC_FOLDER="../static"

#all: pdf html clean
all: html clean

html: main.html

%.html: %.tex refs.bib
	@latexmlc --destination=$(basename $(@F)).xml --noparse $<
	@if [ -d "_XSLT" ]; then \
		latexmlpost --destination=$@ --nodefaultresources --format=html5 --nosplit --stylesheet="./_XSLT/LaTeXML-jekyll-post.xsl" $(basename $(@F)).xml ; \
	else \
		latexmlpost --destination=$@ --nodefaultresources --format=html5 --nosplit --stylesheet="$(STATIC_FOLDER)/_XSLT/LaTeXML-jekyll-post.xsl" $(basename $(@F)).xml ; \
	fi
	@touch -r main.html ../index.md

pdf: main.pdf

%.pdf: %.tex refs.bib
	@latexmk -pdf $<

clean:
	@latexmk -c
	@rm -rf LaTeXML.cache *.bbl *.dvi *.log *.bak *.aux *.blg *.idx *.ps *.eps *.toc *.out *.snm *.nav *.xml *.bcf *.spl *.synctex.gz *~
