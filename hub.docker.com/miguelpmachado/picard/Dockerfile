FROM openjdk:6-jdk-slim
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="1.79-01"

WORKDIR /NGStools/

RUN echo 'deb http://archive.debian.org/debian wheezy main' > /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y wget git ant libbcel-java

RUN wget -nv https://github.com/broadinstitute/picard/archive/1.79.tar.gz && \
    tar xf 1.79.tar.gz && \
    rm 1.79.tar.gz && \
    cd picard-1.79/ && \
    ant

RUN apt-get remove -y wget git ant && \
    apt-get autoclean -y

WORKDIR /data/
