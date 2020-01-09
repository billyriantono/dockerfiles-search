FROM ubuntu:trusty

MAINTAINER Sven SAULEAU <contact@xtuc.fr>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -q
RUN apt-get install -y \
 build-essential \
 git \
 nodejs-legacy \
 npm

RUN npm install -g bower grunt-cli gulp less typescript

WORKDIR /root
