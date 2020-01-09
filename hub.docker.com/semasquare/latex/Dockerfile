FROM ubuntu:18.04

RUN mkdir /workspace

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -qq update && \
    apt-get -qq -y install \
    make \
    texlive \
    texlive-lang-german \
    texlive-latex-extra \
    texlive-bibtex-extra \
    texlive-generic-extra \
    texlive-science \
    latexmk \
    biber \
    gnuplot \
    graphviz \
    pandoc && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /workspace

VOLUME /workspace

CMD ["/usr/bin/make"]
