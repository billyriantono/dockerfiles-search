FROM ubuntu:16.04

MAINTAINER yuhaow97@gmail.com

WORKDIR /workspace

RUN apt-get update && \
    apt-get install -y \
    git \
    gcc-5 \
    g++-5 \
    python \
    openjdk-8-jdk \
    autoconf \
    automake \
    autotools-dev \
    curl \
    libmpc-dev \
    libmpfr-dev \
    libgmp-dev \
    libusb-1.0-0-dev \
    gawk \
    build-essential \
    bison \
    flex \
    texinfo \
    gperf \
    libtool \
    patchutils \
    bc \
    zlib1g-dev \
    device-tree-compiler \
    pkg-config \
    libexpat-dev

ENV WORKSPACE /workspace
ENV LOWRISC_QUICKSTART_PATH $WORKSPACE/lowrisc-quickstart

COPY . $LOWRISC_QUICKSTART_PATH

RUN cd $LOWRISC_QUICKSTART_PATH && \
    make getrelease