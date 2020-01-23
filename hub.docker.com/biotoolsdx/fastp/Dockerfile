FROM ubuntu:16.04
MAINTAINER CHEN, Yuelong <yuelong.chen.btr@gmail.com>

ARG fastp_version=v0.20.0

# install fastp
RUN apt-get update && \
    apt-get install -y git make g++  zlib1g zlib1g-dev
RUN cd /tmp/ && \
    git clone https://github.com/OpenGene/fastp.git && \
    cd fastp && \
    git checkout $fastp_version && \
    make && \
    make install

# clean
RUN rm -rf /tmp/fastp* && \
    apt-get clean && \
    apt-get remove --yes --purge git make g++

CMD fastp