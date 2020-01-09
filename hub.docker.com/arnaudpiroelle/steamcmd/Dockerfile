FROM ubuntu:16.04
MAINTAINER Arnaud Piroelle "piroelle.arnaud@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get -y install lib32gcc1 curl \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

RUN mkdir -p /steamcmd \
    && cd /steamcmd  \
    && curl https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz | tar xvz \
    && ./steamcmd.sh +quit
