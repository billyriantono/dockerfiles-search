FROM ubuntu:bionic

RUN apt update && \
    apt install -y \
    software-properties-common \
    automake \
    autoconf \
    pkg-config \
    libcurl4-openssl-dev \
    libjansson-dev \
    libssl-dev \
    libgmp-dev \
    make \
    g++ \
    git && \
    git clone https://github.com/hyc/cpuminer-multi
WORKDIR /cpuminer-multi
RUN ./autogen.sh && \
    CFLAGS="-march=native" ./configure && \
    make install
