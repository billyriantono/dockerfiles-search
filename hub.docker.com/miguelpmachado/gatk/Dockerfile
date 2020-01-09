FROM openjdk:6-jdk-slim
MAINTAINER Miguel Machado <miguel.machado@insa.min-saude.pt>
LABEL version="1.6-01"

WORKDIR /NGStools/

RUN echo 'deb http://archive.debian.org/debian wheezy main' > /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y wget git ant curl

RUN wget -nv https://github.com/broadgsa/gatk-protected/archive/1.6.tar.gz && \
    tar xf 1.6.tar.gz && \
    rm 1.6.tar.gz && \
    cd gatk-protected-1.6/ && \
    ant

RUN curl -LO 'https://software.broadinstitute.org/gatk/misc/gsamembers_broadinstitute.org.key.zip' && \
    unzip gsamembers_broadinstitute.org.key.zip && \
    rm gsamembers_broadinstitute.org.key.zip

RUN apt-get remove -y wget git ant curl && \
    apt-get autoclean -y

WORKDIR /data/
