FROM ubuntu:14.04
MAINTAINER yookuda <yookuda@nig.ac.jp>
WORKDIR /tmp
RUN apt-get update && \
    apt-get -y install wget gcc make && \
    apt-get clean
RUN cp /usr/include/stdio.h /usr/include/stdio.h~ && \
    sed -i -e 678,680d /usr/include/stdio.h && \
    wget http://lowelab.ucsc.edu/software/tRNAscan-SE-1.23.tar.gz && \
    tar xzvf tRNAscan-SE-1.23.tar.gz && \
    cd tRNAscan-SE-1.23 && \
    export HOME=/usr/local && \
    make && \
    make install && \
    make testrun && \
    make clean && \
    mv /usr/include/stdio.h~ /usr/include/stdio.h && \
    rm -rf /tmp/*
RUN mkdir /data
