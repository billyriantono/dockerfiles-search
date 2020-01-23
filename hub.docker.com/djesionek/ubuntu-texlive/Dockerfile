FROM ubuntu:latest

RUN apt update -y
RUN apt install -y texlive-base \
    texlive-base \
    texlive-bibtex-extra \
    texlive-binaries \
    texlive-extra-utils \
    texlive-font-utils \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-formats-extra \
    texlive-lang-german \
    texlive-lang-english \
    texlive-latex-extra \
    texlive-latex-recommended \
    texlive-luatex \
    texlive-metapost \
    texlive-pictures \
    texlive-pstricks \
    texlive-science \
    biber \
    make

RUN mkdir /build
WORKDIR /build

ENTRYPOINT ./build.sh
