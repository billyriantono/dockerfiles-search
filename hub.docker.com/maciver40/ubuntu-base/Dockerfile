FROM ubuntu:18.04

LABEL maintainer="robert@eisenmann.email"

ADD https://github.com/just-containers/s6-overlay/releases/download/v1.21.8.0/s6-overlay-amd64.tar.gz /tmp/

ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
ENV USER_ID 99
ENV GROUP_ID 100
ENV UMASK 0000

RUN \
    # INSTALL BASIC PACKAGES
    apt-get update && \
    apt-get install -y \
        apt-utils \
        apt-transport-https \
        autoconf \
        autogen \
        automake \
        bash \
        build-essential \
        ca-certificates \
        coreutils \
        cron \
        curl \
        git \
        grep \
        gnupg \
        htop \
        iftop \
        lsb-release \
        mc \
        nano \
        software-properties-common \
        tar \
        tzdata \
        unzip \
        util-linux \
        wget && \
    # SET TIMEZONE
    ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime && \
    # INSTALL S6 OVERLAY    
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && \
    rm -rf /tmp/*
   
COPY /files /
ONBUILD COPY /files /

ENTRYPOINT ["/init"]
