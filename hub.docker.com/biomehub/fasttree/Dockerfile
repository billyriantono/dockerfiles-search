FROM ubuntu:19.04
ENV DEBIAN_FRONTEND noninteractive
MAINTAINER BiomeHub

LABEL version="2.1.10"
LABEL software.version="2.1.10"
LABEL software="Fasttree"

RUN apt-get -y update; \
    apt-get -y upgrade; \
    apt-get -y install fasttree
