FROM ubuntu:latest

MAINTAINER Kameron Ingrando

RUN set -e -x \
    && set export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        ca-certificates \
        curl \
        dumb-init \
        gcc \
        ifupdown \
        inetutils-ping \
        iperf3 \
        iproute2 \
        knot-host \
        net-tools \
        openssh-client \
        python3 \
        python3-dev \
        python3-pip \
        python3-cryptography \
        python3-setuptools \
        python3-wheel \
        telnet \
        traceroute \
        vim-tiny \
    && ln -s /usr/bin/khost /usr/local/bin/host \
    && rm -rf /var/lib/apt/lists/*

VOLUME ["/data"]

