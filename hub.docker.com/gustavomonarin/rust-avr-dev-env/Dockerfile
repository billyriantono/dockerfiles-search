FROM debian:stretch

MAINTAINER Gustavo Monarin de Sousa <gustavomonarin@gmail.com>

RUN apt-get update  \
    && DEBIAN_FRONTEND=noninteractive apt-get install --yes \
        file \
        g++ \
        make \
        cmake \
        curl \
        git \
        python \
        binutils-avr \
        gcc-avr \
        gdb-avr \
        avrdude \
    && apt-get clean

RUN cd /usr/src \ 
    && git clone https://github.com/avr-rust/rust.git \
    && mkdir build && cd build \
    && ../rust/configure \
    && make