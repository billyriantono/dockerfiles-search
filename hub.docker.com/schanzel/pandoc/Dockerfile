FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -y \
  && apt-get install -y --no-install-suggests \
    pandoc \
    pandoc-citeproc \
    texlive-latex-base \
    texlive-xetex \
    texlive-fonts-extra \
    texlive-bibtex-extra \
    fontconfig \
    lmodern

CMD ["/bin/bash"]
