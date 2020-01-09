FROM ubuntu:16.04
MAINTAINER tilldettmering@gmail.com

ADD *.sh /

RUN apt-get update &&\
    apt-get install -y pdftk imagemagick &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/*
