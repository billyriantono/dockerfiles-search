#
# Dockerfile to build the SimGear image
#

FROM debian:jessie AS builder

WORKDIR /simgear

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    libboost-all-dev \
    libglew-dev \
    libopenal-dev \
    ca-certificates \
    git \
    libjpeg-dev \
    libghc-zlib-dev \
    libcurl4-openssl-dev \
    libpng-dev \
    libtiff-dev \
    libcairo-dev \
    pkg-config

#COPY patches /patches

WORKDIR /simgear

RUN git clone  https://github.com/openscenegraph/osg.git \ 
    && cd osg \ 
    && git checkout OpenSceneGraph-3.4 \
    && mkdir build && cd build && cmake -G "Unix Makefiles" \
                              -D CMAKE_BUILD_TYPE=Release \
                              -D CMAKE_PREFIX_PATH="/usr/local" \
                              -D CMAKE_INSTALL_PREFIX:PATH=/usr/local \
                              -D CMAKE_CXX_FLAGS="-pipe" \
                              .. \
    && make && make install && cd ..

RUN git clone --depth 1 https://git.code.sf.net/p/flightgear/simgear \
    && cd simgear \
    && mkdir build && cd build && cmake -G "Unix Makefiles" \
                              -D CMAKE_BUILD_TYPE=Release \
                              -D CMAKE_PREFIX_PATH="/usr/local" \
                              -D CMAKE_INSTALL_PREFIX:PATH=/usr/local \
                              -D CMAKE_CXX_FLAGS="-pipe" \
                              -D ENABLE_RTI=OFF \
                              -D ENABLE_DNS=ON \
                              .. \
    && make && make install

