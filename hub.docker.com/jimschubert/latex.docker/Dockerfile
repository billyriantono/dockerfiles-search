FROM ubuntu:17.04

MAINTAINER Jim Schubert <james.schubert@gmail.com>

RUN mkdir -p /src \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
    wget xzdec tidy \
    make imagemagick inkscape pandoc python-pygments \
    texlive-binaries texlive-fonts-recommended texlive-generic-recommended \
    texlive-htmlxml texlive-lang-english texlive-latex-base texlive-luatex \
    texlive-pictures texlive-plain-extra texlive-pstricks texlive-publishers texlive-formats-extra \
    texlive-generic-recommended lmodern \
    texlive-latex-recommended texlive-xetex tipa tk8.6-blt2.5 \
    ttf-adf-accanthis ttf-adf-gillius ttf-adf-universalis tzdata \
    t1utils tex-common tex-gyre texinfo texlive-base texlive-extra-utils \
    && rm -rf /var/lib/apt/lists/*

RUN tlmgr init-usertree \
    && tlmgr update --self \
    && tlmgr install fontawesome

VOLUME /src
