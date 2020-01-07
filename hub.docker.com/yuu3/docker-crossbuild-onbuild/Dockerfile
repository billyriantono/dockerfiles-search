FROM ubuntu:16.04
MAINTAINER yuu

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    sudo ca-certificates locales \
    bzip2 xz-utils \
    python python3 \
    cmake make \
    && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND dialog

ENV LANG=en_US.UTF-8
ENV LC_ALL=$LANG
RUN sed -ie 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    locale-gen --purge $LANG && \
    locale-gen && update-locale LANG=$LANG LC_ALL=$LC_ALL

RUN ln -sf /usr/bin/python3 /usr/bin/python
RUN ln -sf /bin/bash /bin/sh

ONBUILD ADD toolchain.sh /
ONBUILD RUN chmod +x toolchain.sh && /toolchain.sh -y && rm /toolchain.sh
