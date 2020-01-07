FROM golang:1.7

RUN apt-get update -y \
  && apt-get install -y --no-install-recommends \
    pandoc \
    texlive-binaries \
    texlive-latex-base \
    texlive-fonts-recommended \
    texlive-fonts-extra \
    latexmk \
    lmodern \
    texlive-xetex \
    fonts-arphic-bkai00mp \
    fonts-arphic-gbsn00lp \
    fonts-arphic-bsmi00lp \
    fonts-arphic-gkai00mp \
    fonts-arphic-uming \
    fonts-arphic-ukai \
    fontconfig && fc-cache -fv
