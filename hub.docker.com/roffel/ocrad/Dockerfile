FROM ubuntu:latest
MAINTAINER Rutger Roffel <info@roffel.info>
RUN apt-get -y update && apt-get -qq update && apt-get -qq install time && apt-get -qq install make && apt-get install -qq build-essential

RUN apt-get install lzip wget -qq \
    && mkdir /temporary \
    && cd /$_ \
    && wget "http://ftp.snt.utwente.nl/pub/software/gnu/ocrad/ocrad-0.26.tar.lz" \
    && lzip -cd ocrad-0.26.tar.lz | tar -xf - \
    && cd ocrad-0.26 \
    && ./configure && make && make install \
    && rm -rf /temporary \
    && cd / \
    && apt-get -qq remove wget \
    && apt-get -qq remove lzip