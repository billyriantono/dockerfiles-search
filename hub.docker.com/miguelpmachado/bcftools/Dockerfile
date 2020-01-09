FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="1.9-01"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y wget gcc make bzip2 libncurses5-dev zlib1g-dev libbz2-dev liblzma-dev

RUN wget -nv https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2 && \
    tar xf bcftools-1.9.tar.bz2 && \
    cd bcftools-1.9 && \
    ./configure && \
    make && \
    make install && \
    make clean && \
    cd /NGStools && \
    rm bcftools-1.9.tar.bz2

RUN apt-get remove -y wget gcc make && \
    apt-get autoclean -y

WORKDIR /data/
