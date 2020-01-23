FROM ubuntu:14.04
MAINTAINER David Li <davidli012345@gmail.com>

RUN apt-get update && apt-get install -y autoconf automake gcc g++ make gfortran wget curl

RUN cd /usr/local/src/ && \
    wget http://www.mpich.org/static/downloads/3.2/mpich-3.2.tar.gz && \
    tar xf mpich-3.2.tar.gz && \
    rm mpich-3.2.tar.gz && \
    cd mpich-3.2 && \
    ./configure && \
    make && make install && \
    cd /usr/local/src && \
    rm -rf mpich-3.2

ENV PATH=/usr/bin:/usr/local/bin:/bin:/app
