FROM ubuntu:18.04

LABEL version="2.0"

WORKDIR /tex

RUN echo "Europe/Zurich" > /etc/timezone
ENV DEBIAN_FRONTEND=noninteractive

# Installing latex related stuff and also python and pygmentize for minted
RUN apt-get update && apt-get install --no-install-recommends -y \
    biber \
    git \
    latexmk \
    make \
    texlive \
    texlive-xetex \
    texlive-latex-extra \
    texlive-bibtex-extra \
    texlive-generic-extra \
    texlive-science \
    python-pygments \
    texlive-lang-european \
    texlive-lang-german \
    texlive-lang-french \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install --no-install-recommends -y openssh-client


ENTRYPOINT [ "latexmk", "-pdf", "-shell-escape" ]

