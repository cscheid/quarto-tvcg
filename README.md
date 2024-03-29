# A quarto template for IEEE VIS journal submissions (TVCG)

With this repository, you'll be able to create submissions for [IEEE
VIS](https://ieeevis.org) using [Quarto](https://quarto.org).

With this template and quarto, you can:

* generate publication-ready PDF files as well as HTML
  documents from the same source
  
* ensure computational reproducibility by including computational
  content with the source of the paper, which gets executed every time
  the paper is recompiled
  
  
## Installation Requirements

* [Quarto](https://quarto.org)

* If you intend to run R code chunks, you'll need a recent version of
  R. [Pre-release versions of RStudio](https://dailies.rstudio.com/)
  offer native support for Quarto, but R is not at all required to run
  Quarto at all if you don't intend to use R code.

* If you intend to run Python code chunks, you'll need to install
  [Jupyter](https://jupyter.org/).

* If you intend to run both Python and R in the same document, you'll
  need to install the R package `reticulate`.

This template is heavily based on the LaTeX template files, by authors
below. The full README for that template follows.

## Getting started

The files you'll need are all under `src/`. After you've installed the
requirements, you should be able to

    $ cd src
    $ quarto render paper.qmd

This will produce a `src/paper.pdf` document.

If you start by forking this repository, then you can get going right
away by editing `src/paper.qmd`.

### Producing an HTML version of the file

At any point, you can create an HTML version of the file by uncommenting
the `html: default` line from the front matter in `src/paper.qmd`. Alternatively,
you can simply type

    $ quarto render paper.qmd --to html

This will produce a `paper.html` and `paper_files` subdirectory with the necessary
HTML resources. The links in quarto HTML documents are all relative, so copying
the file and its folder to a web page should be enough.

#### Customization

If you want to control the look and feel of your HTML document, Quarto
offers extensive theming. Please refer [to the documentation and
tutorials](https://quarto.org) for details.

# Feedback

This is an early release. If you run into trouble, please don't
hesitate to file a GitHub issue. 


--------------------------------------------------------------------------------
# Old Readme

Created by Torsten Moeller (vis@cs.sfu.ca), April 6 2004
modified by Steven Bergner and Torsten Moeller, June 30 2006
modified by James Peltier and Torsten Moeller, March 28, 2007
modified by Bernhard Finkbeiner, July 5, 2010
modified by Tobias Isenberg, January 2016
modified by Filip Sadlo, March 2016
modified by Tobias Isenberg, July 2016

This distribution provides a document class for formatting papers according to the specifications for submission to conferences sponsored by the IEEE Visualization & Graphics Technical Committee (VGTC).

Conferences that use the 'journal' document option:
- IEEE Visualization Conference (VIS, incl. InfoVis, SciVis, VAST)
- IEEE Virtual Reality (VR)
- IEEE International Symposium on Mixed and Augmented Reality (ISMAR)

It contains 13 files/directories:

README          - this file
diamondrule.eps - abstract and body separator
diamondrule.pdf - its PDF version
vgtc.cls        - the VGTC class file, which should be placed, somewhere in the TeX search path (or in the local directory)
template.tex    - an example paper
template.bib    - a small bibliography file used by the example
template.pdf    - an example proper pdf output in default journal mode
abbrv-doi*.bst  - four different versions to generate the bibliography including DOI output, with and without hyperref support, with and without narrow rendering of DOIs
makefile        - makefile including bibtex compilation and proper PDF generation
pictures/       - subdirectory with sample images, both in EPS and in direct pixel/vector format

Usage
=====

The template can be used as such (using the established LaTeX environments) by calling pdfLaTeX or LaTex. For Windows-based LaTeX installations you can use, for example, the environment provided by http://www.texniccenter.org/ along with MikTeX (http://miktex.org/). For Uinux-based installations, please use your favorite LaTeX distribution and editing environment or use the makefile following the instructions below.

Use of the Makefile
===================

Prior to "building" a paper please be sure to run

  make clean

This will ensure that the paper is built cleanly each and every time. We suggest to run this command before each new compilation.

To compile the example, run

  make

or manually, if the makefile does not work for you

  latex template
  bibtex template
  latex template
  latex template

If you run 'make' for the first time, a successful compilation will create a file called 'template.pdf'. Please make sure, that its layout is identical to the file 'template-journal.pdf' provided with this package.

The included makefile also allows you to run each step of the process manually.  Below are a list of available options that may be passed to make

 "make clean"
   removes all files that can be generated automatically.

 "make gs7"
   This will perform all functions to build a proper paper using GhostScript 7.

 "make gs8"
   This will perform all functions to build a proper paper using GhostScript 8.

 "make dvi"
   This will process the .tex file and produce a DVI output file.  This
   step may process the .tex file several times to process all references
   and citations.

 "make ps"
   This will process the .tex file and the DVI output and convert it to a
   PostScript file.

 "make pdf"
   This will process the .tex file using pdfTeX/pdflatex to produce a PDF
   file directly (not using a DVI and PostScript file).
   Please make sure that all fonts are embedded.
   You can use pdffonts my_document.pdf to check if they are.
   It is standard in all modern latex distributions.
   If you use eps figures (e.g. R or gnuplot figures) which you convert to
   PDF using epstopdf, do the following:
   Use GL_OPTIONS, a global environment variable for ghostscript:
   export GS_OPTIONS="-dEmbedAllFonts=true -dPDFSETTINGS=/printer"
   # and run
   epstopdf myfile.eps

   See http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=411651 for the
   origin of this solution.


If you have problems with the makefile please notify us with the output of
the errors produced when running make and we will work to figure out the
resolution.


To produce proper pdf output, please use:
  dvips -t letter -Pdownload35 -Ppdf -G0 template.dvi -o template.ps

The "-Ppdf" and "-G0" flags should be specified in that order; reversing
them does not work, and will result in unacceptable results.

The following information is an exerpt from the ACM SIGGRAPH Conference /
Symposium / Workshop Content Formatting Instructions which can be found
here.

 http://www.siggraph.org/publications/instructions/author-instructions.pdf

If you are using version 7.x of GhostScript, please use the following
method of invoking ‘ps2pdf,’ in order to embed all typefaces and ensure
that images are not downsampled or subsampled in the PDF creation process:

 ps2pdf -dCompatibilityLevel=1.3 -dMaxSubsetPct=100 \
        -dSubsetFonts=true -dEmbedAllFonts=true \
        -dAutoFilterColorImages=false -dAutoFilterGrayImages=false \
        -dColorImageFilter=/FlateEncode -dGrayImageFilter=/FlateEncode \
        -dMonoImageFilter=/FlateEncode template.ps template.pdf

If you are using version 8.x of GhostScript, please use this method in
place of the example above:

 ps2pdf -dPDFSETTINGS=/prepress -dCompatibilityLevel=1.3 \
        -dAutoFilterColorImages=false -dAutoFilterGrayImages=false \
        -dColorImageFilter=/FlateEncode -dGrayImageFilter=/FlateEncode \
        -dMonoImageFilter=/FlateEncode template.ps template.pdf

This has been incorporated into the makefile and should no longer be needed
unless you are building the PDF file manually.
