FROM ubuntu

RUN apt-get update -y
RUN apt-get install -y pandoc pandoc-citeproc texlive-latex-base texlive-xetex latex-xcolor texlive-math-extra texlive-latex-extra texlive-fonts-extra texlive-bibtex-extra biber

RUN mkdir /source
WORKDIR /source

ENTRYPOINT ["/usr/bin/pandoc"]
