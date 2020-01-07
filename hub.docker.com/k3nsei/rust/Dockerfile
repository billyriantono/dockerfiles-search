FROM rust:1-stretch

RUN DEBIAN_FRONTEND=noninteractiv
RUN apt-get update
RUN apt-get install g++ make binutils autoconf automake autotools-dev libtool pkg-config \
    zlib1g-dev libcunit1-dev libssl-dev libxml2-dev libev-dev libevent-dev libjansson-dev \
    libc-ares-dev libjemalloc-dev libsystemd-dev screen xvfb \
    cython python3-dev python-setuptools -y --force-yes

WORKDIR /tmp
RUN wget https://github.com/nghttp2/nghttp2/releases/download/v1.32.0/nghttp2-1.32.0.tar.bz2 -O - | tar -xj

WORKDIR /tmp/nghttp2-1.32.0
RUN ./configure; \
    make; \
    make install;

WORKDIR /
