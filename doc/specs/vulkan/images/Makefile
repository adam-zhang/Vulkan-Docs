# This Makefile should be used to regenerate alternate forms of
# documents when the source changes. Note that pipeline.* is
# treated specially since its original source format is .pptx
#
# Targets:
#   all - regenerate all images from source formats
#   clean - remove all generated images
#   individual files in $(TARGETS) below

# Default rules go from Inkscape SVG -> PDF.
# Some bashing is required for vulkanpipeline.*, which originally
# comes from PowerPoint -> export to PDF -> convert to SVG. Converting
# the other way using inkscape just does not work - horrible drop
# shadows everywhere.

#.SUFFIXES: .pdf .svg

#.svg.pdf: ; $(INKSCAPE) -f $< -A $@

# Tool to convert image formats
INKSCAPE ?= inkscape

# PDFs to regenerate from SVGs - everything except pipeline.pdf
SVGEXCLUDES = pipeline.svg vulkantexture0.svg
SVGSRC = $(filter-out $(SVGEXCLUDES),$(wildcard [A-Za-z]*.svg))
PDFDST = $(SVGSRC:%.svg=%.pdf)
SVGDST = pipeline.svg

all: $(PDFDST) $(SVGDST)

$(PDFDST): %.pdf: %.svg
	$(INKSCAPE) -f $< -A $@

pipeline.svg: pipeline.pdf
	$(INKSCAPE) -f $< -l $@

clean:
	-rm -f $(PDFDST) $(SVGDST)
