FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="0.7.9a-01"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y wget bzip2 make gcc zlib1g-dev

RUN wget -nv https://downloads.sourceforge.net/project/bio-bwa/bwa-0.7.9a.tar.bz2 && \
    tar xf bwa-0.7.9a.tar.bz2 && \
    cd bwa-0.7.9a && \
    make && \
    cd .. && \
    rm bwa-0.7.9a.tar.bz2

ENV PATH="/NGStools/bwa-0.7.9a:${PATH}"

RUN apt-get remove -y wget make gcc && \
    apt-get autoclean -y

WORKDIR /data/
