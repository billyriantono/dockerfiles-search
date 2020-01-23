FROM debian:stretch-20171210

LABEL maintainer="Ayoob Buildroot" \
description="Graphicalinfo.com Container with everything needed to run Buildroot for raspberry pi 3 b+"

# Setup environment
ENV DEBIAN_FRONTEND noninteractive

# This repository can be a bit slow at times. Don't panic...
COPY apt-sources.list /etc/apt/sources.list

# The container has no package lists, so need to update first
RUN dpkg --add-architecture i386 && \
    apt-get update -y
RUN apt-get install -y --no-install-recommends \
        bc \
        build-essential \
        bzr \
        ca-certificates \
        cmake \
        cpio \
        cvs \
        file \
        g++-multilib \
        git \
        libc6:i386 \
        libncurses5-dev \
        locales \
        mercurial \
        python-flake8 \
        python-nose2 \
        python-pexpect \
        python3 \
        python3-nose2 \
        python3-pexpect \
        qemu-system-arm \
        qemu-system-x86 \
        rsync \
        subversion \
        unzip \
        wget \
        && \
    apt-get -y autoremove && \
    apt-get -y clean

# To be able to generate a toolchain with locales, enable one UTF-8 locale
RUN sed -i 's/# \(en_US.UTF-8\)/\1/' /etc/locale.gen && \
    /usr/sbin/locale-gen

RUN useradd -ms /bin/bash ayoob && \
    chown -R ayoob:ayoob /home/ayoob

USER ayoob
WORKDIR /home/ayoob
ENV HOME /home/ayoob
ENV LC_ALL en_US.UTF-8

RUN git clone https://github.com/buildroot/buildroot  && \
cd buildroot && \
make raspberrypi3_defconfig
