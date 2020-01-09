FROM ubuntu:latest

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
    texlive-full \
    make \
    git \
    wget \
    curl \
    fontconfig \
    texlive-fonts-extra \
    texlive-latex-extra \
    texlive-math-extra \
    latex-xcolor \
    texlive-xetex && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT /bin/bash
