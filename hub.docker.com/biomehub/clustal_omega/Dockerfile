FROM ubuntu:19.04
ENV DEBIAN_FRONTEND noninteractive
MAINTAINER BiomeHub

LABEL version="1.2.4"
LABEL software.version="1.2.4"
LABEL software="ClustalOmega"

RUN apt-get -y update; \
    apt-get -y upgrade; \
    apt-get -y install clustalo
