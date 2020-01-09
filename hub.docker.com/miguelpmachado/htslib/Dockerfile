FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="1.9"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y wget gcc make bzip2 zlib1g-dev libbz2-dev liblzma-dev

RUN wget -nv https://github.com/samtools/htslib/releases/download/1.9/htslib-1.9.tar.bz2 && \
    tar xf htslib-1.9.tar.bz2 && \
    cd htslib-1.9 && \
    ./configure && \
    make && \
    make install && \
    make clean && \
    cd /NGStools && \
    rm htslib-1.9.tar.bz2

RUN apt-get remove -y wget gcc make && \
    apt-get autoclean -y

WORKDIR /data/
