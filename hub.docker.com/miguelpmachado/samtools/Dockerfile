FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="0.1.18-01"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y wget make gcc zlib1g-dev libncurses5-dev

RUN wget -nv https://github.com/samtools/samtools/archive/0.1.18.tar.gz && \
    tar xf 0.1.18.tar.gz && \
    rm 0.1.18.tar.gz && \
    cd samtools-0.1.18 && \
    make

ENV PATH="/NGStools/samtools-0.1.18:/NGStools/samtools-0.1.18/bcftools:/NGStools/samtools-0.1.18/misc:${PATH}"

RUN apt-get remove -y wget make gcc  && \
    apt-get autoclean -y

WORKDIR /data/
