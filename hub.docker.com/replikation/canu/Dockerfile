FROM ubuntu:bionic
ENV DEBIAN_FRONTEND=noninteractive
MAINTAINER Christian Brandt <christian.jena@gmail.com>

RUN apt-get update && apt-get install -y \
        git \
        g++ \
        make \
        openjdk-8-jdk

RUN git clone https://github.com/marbl/canu.git && \
    cd canu/src && \
    make

ENV PATH /canu/Linux-amd64/bin/:$PATH
