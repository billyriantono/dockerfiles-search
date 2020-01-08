FROM openjdk:14-alpine

MAINTAINER Simon Balzer version: 0.1

WORKDIR /work
RUN apk update 
RUN apk add git make wget tar
RUN wget -q -O eclipse.tar.gz "mirror.dkm.cz/eclipse/technology/epp/downloads/release/2019-09/R/eclipse-cpp-2019-09-R-linux-gtk-x86_64.tar.gz" && tar -xzf eclipse.tar.gz && rm eclipse.tar.gz

RUN mkdir /workspace
VOLUME /workspace