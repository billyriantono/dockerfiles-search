FROM debian:stretch-slim

MAINTAINER RayBa "rainerbaun@gmail.com"

#Don't ask questions during install
ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8

RUN apt update \
    && apt -y install \
    locales && \
    locale-gen C.UTF-8 && \
    /usr/sbin/update-locale LANG=C.UTF-8 && \
    apt-get remove -y locales