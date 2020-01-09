#FROM nvidia/cuda:10.0-devel-ubuntu16.04 as builder
FROM nvidia/cuda:9.1-devel-ubuntu16.04 as builder

# Set the env variable DEBIAN_FRONTEND to noninteractive
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        cmake \
        build-essential \
        git \
        libx11-dev \
        nasm

RUN cd tmp && \
    git clone --depth 1 https://chromium.googlesource.com/libyuv/libyuv && \
    cd libyuv &&\
    make -f linux.mk libyuv.a && cp libyuv.a /usr/lib/x86_64-linux-gnu && cd include && cp -r * /usr/include

ADD . /opt/sources
RUN cd /opt/sources && \
    mkdir build && cd build && \
    cmake -D CMAKE_INSTALL_PREFIX=/usr .. && make && make install
