# Copyright (C) 2019  Christian Berger

FROM nvidia/cuda:10.1-devel-ubuntu18.04 as builder

# Set the env variable DEBIAN_FRONTEND to noninteractive
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get dist-upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        cmake \
        build-essential && \
    apt-get clean

ADD . /opt/sources
WORKDIR /opt/sources
RUN mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr .. && \
    make && make install

ENTRYPOINT ["/usr/bin/video-nvenc-h264-recorder"]
