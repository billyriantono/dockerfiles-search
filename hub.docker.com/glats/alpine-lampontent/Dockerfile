FROM ubuntu:16.04

RUN dpkg --add-architecture i386
RUN apt-get update -y && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends software-properties-common
RUN add-apt-repository ppa:ubuntu-wine/ppa
RUN apt-get update -y && apt-get install --no-install-recommends -y wine1.8 winetricks winbind git nodejs npm
RUN npm i -g n
RUN n latest
