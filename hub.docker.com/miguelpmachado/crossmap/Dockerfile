FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="0.3.9"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y wget python3 python3-pip libbz2-dev liblzma-dev libcurl4-gnutls-dev zlib1g-dev

RUN pip3 install setuptools pyBigWig numpy

RUN wget -nv https://downloads.sourceforge.net/project/crossmap/CrossMap-0.3.9.tar.gz && \
    tar xf CrossMap-0.3.9.tar.gz && \
    cd CrossMap-0.3.9 && \
    python3 setup.py install && \
    cd /NGStools && \
    rm CrossMap-0.3.9.tar.gz

WORKDIR /chain_files/human/

RUN wget -nv ftp://ftp.ensembl.org/pub/assembly_mapping/homo_sapiens/*.chain.gz

RUN pip3 uninstall setuptools

RUN apt-get remove -y wget python3-pip && \
    apt-get autoclean -y

WORKDIR /data/
