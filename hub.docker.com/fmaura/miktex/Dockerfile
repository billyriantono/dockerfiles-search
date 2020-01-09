FROM debian:buster-slim

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y \
            texlive \
            texlive-lang-english \
            texlive-lang-german \
            texlive-latex-extra \
            texlive-bibtex-extra \
            biber \
            latexmk
RUN fmtutil-sys --all
RUN apt-get install -y make
