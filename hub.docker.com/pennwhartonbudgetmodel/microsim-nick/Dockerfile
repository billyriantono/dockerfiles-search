FROM ubuntu:latest
MAINTAINER Nick Janetos "njanetos@wharton.upenn.edu"

RUN apt-get update
RUN apt-get install -y python3 python3-pip git wget

RUN mkdir repo
ADD . / repo/

RUN cd repo && pip3 install -r requirements.txt

RUN wget https://dl.bintray.com/boostorg/release/1.65.1/source/boost_1_65_1.tar.bz2 && \
    tar --bzip2 -xf boost_1_65_1.tar.bz2 && \
    mkdir boost && \
    cd boost_1_65_1 && \
    ./bootstrap.sh --with-python=python3.6 --prefix=~/boost && \
    ./b2 stage && \
    cd .. && \
    rm boost_1_65_1.tar.bz2
