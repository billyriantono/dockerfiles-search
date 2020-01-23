FROM ubuntu:latest

RUN apt-get update && apt-get install -y\
	texlive texlive-bibtex-extra texlive-fonts-extra texlive-generic-extra texlive-lang-english texlive-lang-german texlive-lang-spanish texlive-latex-extra texlive-pstricks texlive-publishers texlive-science latexmk biber\
	gnuplot python git\
	python-numpy python-scipy python-matplotlib python-skimage python-pip\
	make\
	openjdk-9-jre\
	blender\
	ghostscript libtiff-tools

RUN pip install peakutils tqdm