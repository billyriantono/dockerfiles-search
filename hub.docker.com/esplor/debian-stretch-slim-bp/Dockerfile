FROM debian:stretch-slim

RUN echo 'deb http://deb.debian.org/debian stretch-backports main' > /etc/apt/sources.list.d/backports.list \
    && ln -sf /usr/share/zoneinfo/Europe/Oslo /etc/localtime \
    && apt-get update \
    && apt-get --auto-remove -y dist-upgrade \
    && rm -rf /var/lib/apt/lists/*
