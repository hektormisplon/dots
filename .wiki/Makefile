entries := $(wildcard *.md)

target=wiki
exports= \
  $(entries:.md=.html) \
	# $(target).pdf  \

VIMWIKI_DIR=/home/h/.wiki

all: $(exports)

%.html:%.md
	pandoc																										 \
	 -f markdown																							 \
	 -t html5																									 \
	 -c pandoc.css																						 \
	 --pdf-engine=xelatex																			 \
	 --bibliography $(VIMWIKI_DIR)/references.bib							 \
	 --citeproc																								 \
	 --lua-filter=$(VIMWIKI_DIR)/filters/html-links.lua        \
	 --lua-filter=$(VIMWIKI_DIR)/filters/diagram-generator.lua \
	 --lua-filter=$(VIMWIKI_DIR)/filters/lilypond.lua          \
	 --mathjax																								 \
	 --extract-media=diagrams																	 \
	 -s -o $@ $<

$(target).pdf:$(entries)
	pandoc \
		-f markdown $(entries)                       \
		--pdf-engine=xelatex                         \
		--bibliography $(VIMWIKI_DIR)/references.bib \
		--citeproc                                   \
		--table-of-contents                          \
		-o $@

# clean:
# 	rm -f *.html
# 	rm wiki.pdf
