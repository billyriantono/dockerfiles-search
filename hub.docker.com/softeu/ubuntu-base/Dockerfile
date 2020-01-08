FROM ubuntu:14.04

MAINTAINER Jindrich Vimr <jvimr@softeu.com>

ENV DEBIAN_FRONTEND noninteractive
RUN echo "1.565.1" > .lts-version-number

RUN apt-get update && apt-get install -y wget git curl zip vim subversion


RUN echo "Europe/Prague" > /etc/timezone

RUN apt-get -qqy install language-pack-en &&    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8


