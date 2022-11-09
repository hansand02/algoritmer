.PHONY = all pdf svg mildclean clean

HEADER := $(realpath -f tex_files/header.tex)
FOOTER := $(realpath -f tex_files/footer.tex)

COMPILEDIR := .compile_dir
PDFCC = texfot --quiet xelatex --output-dir $(COMPILEDIR) -interaction=nonstopmode

TEXS := $(wildcard søk/pseudo/*.tex) \
		$(wildcard trær/pseudo/*.tex) \
		$(wildcard bst/pseudo/*.tex) \
		$(wildcard avl/pseudo/*.tex) \
		$(wildcard heap/pseudo/*.tex) \
		$(wildcard graf/pseudo/*.tex) \
		$(wildcard sort/pseudo/*.tex) \
		$(wildcard hash/pseudo/*.tex) \

PDFS := $(TEXS:%.tex=%.pdf)
SVGS := $(TEXS:%.tex=%.svg)

TOSS := $(TEXS:%.tex=%*.aux) \
		$(TEXS:%.tex=%*.log) \
		$(TEXS:%.tex=%*.nav) \
		$(TEXS:%.tex=%*.out) \
		$(TEXS:%.tex=%*.snm) \
		$(TEXS:%.tex=%*.synctex.gz) \
		$(TEXS:%.tex=%*.toc) \
		$(TEXS:%.tex=%*.vrb)

all: $(PDFS) $(SVGS)

pdf: $(PDFS)

svg: $(SVGS)

mildclean:
	-@rm -f $(TOSS)
	-@rm -rf $(COMPILEDIR)

clean: mildclean
	-@rm -f $(PDFS)
	-@rm -f $(SVGS)

%.pdf: %.tex
	@mkdir -p $(COMPILEDIR)
	@cat $(HEADER) $< $(FOOTER) > $(COMPILEDIR)/$(shell basename $<)
	@$(PDFCC) $(COMPILEDIR)/$(shell basename $<)
	@mv $(COMPILEDIR)/$(shell basename $*).pdf $@

%.svg: %.pdf
	@pdf2svg $< $@
