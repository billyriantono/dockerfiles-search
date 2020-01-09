FROM ubuntu:16.04

RUN dpkg --add-architecture i386 \
    && apt-get -y update \
    && apt-get -y install curl wget zip unzip lib32gcc1 libcurl3:i386 libcurl3-gnutls:i386 ca-certificates \
    && apt-get clean \
    && apt-get autoclean

ENV HOME /mnt/server

RUN ln -s /usr/lib/x86_64-linux-gnu/libcurl.so.3 /usr/lib/x86_64-linux-gnu/libcurl.so