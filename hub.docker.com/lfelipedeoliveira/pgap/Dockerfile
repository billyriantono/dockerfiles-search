FROM debian:jessie
MAINTAINER lfelipedeoliveira, felipe@lfelipedeoliveira.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y; \
    apt-get install -y openjdk-7-jre-headless file; \
    apt-get install -y gcc; \
    apt-get install -y make; \
    apt-get install -y unzip; \
    apt-get install -y wget; \
    apt-get install -y bioperl; \
    apt-get clean

RUN wget https://github.com/lfelipedeoliveira/biodockers/archive/master.zip --no-check-certificate; \
    unzip master.zip; \
    tar xzf biodockers-master/pgap-modif.tar.gz --directory /; \
    mv pgap-1.12/ pgap


RUN wget http://mafft.cbrc.jp/alignment/software/mafft-7.245-with-extensions-src.tgz; \
    tar xzf /mafft-7.245-with-extensions-src.tgz

WORKDIR /mafft-7.245-with-extensions/core
RUN make clean; \
    make; \
    make install

WORKDIR /

RUN wget http://evolution.gs.washington.edu/phylip/download/phylip-3.696.tar.gz; \
    tar xzf phylip-3.696.tar.gz; \
    mv phylip-3.696 phylip

WORKDIR /phylip/src
RUN make -f Makefile.unx install
WORKDIR /


RUN wget http://micans.org/mcl/src/mcl-14-137.tar.gz; \
    tar xzf mcl-14-137.tar.gz; \
    mkdir /mcl
WORKDIR /mcl-14-137
RUN ./configure --prefix=/mcl; \
    make install

WORKDIR /

RUN wget ftp://ftp.ncbi.nih.gov/blast/executables/release//2.2.12/blast-2.2.12-x64-linux.tar.gz; \
    tar xzvf /blast-2.2.12-x64-linux.tar.gz; \


RUN rm -r biodockers-master; \
    rm /master.zip; \
    rm /mafft-7.245-with-extensions-src.tgz; \
    rm -r /mafft-7.245-with-extensions; \
    rm /phylip-3.696.tar.gz; \
    rm /mcl-14-137.tar.gz; \
    rm /blast-2.2.12-x64-linux.tar.gz

RUN (echo y;echo o conf prerequisites_policy follow;echo o conf commit)|cpan; \
    cpan Bio::AlignIO; \
    cpan Statistics::LineFit; \
    cpan Statistics::Distributions; \
