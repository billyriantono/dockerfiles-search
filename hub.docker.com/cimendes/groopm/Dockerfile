FROM ubuntu:16.04
MAINTAINER Inês Mendes <cimendes@medicina.ulisboa.pt>


RUN  apt-get update && apt-get install -y apt-utils

RUN apt-get -y install git build-essential \
    zlib1g-dev python-numpy python-pip python-dev cython libhdf5-dev \
    libfreetype6-dev libpng-dev python-pillow python-matplotlib \
    libblas-dev liblapack-dev gfortran
RUN apt-get -y install wget

WORKDIR /NGStools

# INSTALL SAMTOOLS

RUN apt-get -y install libncurses5-dev libncursesw5-dev libbz2-1.0 libbz2-dev libbz2-ocaml libbz2-ocaml-dev liblzma-dev

RUN wget https://sourceforge.net/projects/samtools/files/samtools/1.9/samtools-1.9.tar.bz2
RUN tar xf samtools-1.9.tar.bz2 && rm samtools-1.9.tar.bz2
RUN cd samtools-1.9 && make && make install

WORKDIR /NGStools

# INSTALL BWA

RUN git clone https://github.com/lh3/bwa.git
RUN cd bwa; make

WORKDIR /NGStools

# INSTALL BAMMM

RUN apt-get -y install git automake build-essential zlib1g-dev python2.7-numpy libtool

RUN git clone https://github.com/Ecogenomics/BamM.git

RUN cd BamM && python setup.py install


RUN git clone https://github.com/Ecogenomics/GroopM.git

RUN pip install tables

RUN apt-get -y install python-scipy

RUN cd GroopM && python setup.py install