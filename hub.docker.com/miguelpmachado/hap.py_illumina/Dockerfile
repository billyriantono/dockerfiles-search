FROM ubuntu:16.04
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="0.3.10-8-gdac84d9-02"

WORKDIR /NGStools/

RUN apt-get update

RUN apt-get install -y git python cmake bzip2 g++ libbz2-dev zlib1g-dev autoconf wget ant default-jdk python-pip \
        python-scipy python-pandas liblzma-dev && \
    pip install cython numpy pybedtools pysam bx-python

RUN git clone https://github.com/Illumina/hap.py.git && \
    cd hap.py && \
    python install.py --with-rtgtools --no-tests /NGStools/hap.py/installation

ENV PATH="/NGStools/hap.py/installation/bin:/NGStools/hap.py/installation/libexec/rtg-tools-install:${PATH}"

RUN apt-get remove -y git cmake g++ autoconf wget ant python-pip && \
    apt-get autoclean -y

WORKDIR /data/
