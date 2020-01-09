FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive
RUN echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
    fonts-lmodern \
    haskell-platform \
    lmodern \
    msttcorefonts \
    pandoc \
    pandoc-citeproc \
    tex-common \
    tex-gyre \
    texlive \
    texlive-lang-spanish \
    texlive-publishers \
    texlive-science \
    texlive-xetex \
    wget \
    xzdec
