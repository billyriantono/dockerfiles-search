# base - Base Image with Debian 7.0 wheezy

FROM debian:wheezy
MAINTAINER Andres Cazau <cazaua@gmail.com>

RUN apt-get update && apt-get install -y \
    locales

RUN dpkg-reconfigure locales && \
    locale-gen C.UTF-8 && \
    /usr/sbin/update-locale LANG=C.UTF-8

ENV LC_ALL C.UTF-8