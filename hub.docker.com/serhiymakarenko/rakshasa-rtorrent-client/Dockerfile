# The MIT License
#
# Copyright (c) 2019, Serhiy Makarenko

FROM debian:10-slim AS builder

ARG RTORRENT_VERSION=0.9.8
ARG LIBTORRENT_VERSION=0.13.8

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends --no-install-suggests \
    curl file binutils pkg-config libxmlrpc-c++8-dev libssl-dev libcurl4-openssl-dev libncurses5-dev zlib1g-dev build-essential ca-certificates && \
    curl -RL -O "http://rtorrent.net/downloads/libtorrent-${LIBTORRENT_VERSION}.tar.gz" && \
    tar xvzf libtorrent-${LIBTORRENT_VERSION}.tar.gz && \
    cd libtorrent-${LIBTORRENT_VERSION} && \
    ./configure && \
    make && \
    make install-strip && cd ../ && \
    curl -RL -O "http://rtorrent.net/downloads/rtorrent-${RTORRENT_VERSION}.tar.gz" && \
    tar xvzf rtorrent-${RTORRENT_VERSION}.tar.gz && \
    cd rtorrent-${RTORRENT_VERSION} && \
    ./configure \
        --with-xmlrpc-c && \
    make && \
    make install-strip

FROM debian:10-slim
LABEL maintainer="serhiy@makarenko.me"

ARG DEBIAN_FRONTEND=noninteractive

ENV LD_LIBRARY_PATH=/usr/local/lib

RUN apt-get update && \
    apt-get install -y --no-install-recommends --no-install-suggests \
    libcurl4 libncurses5 libxmlrpc-c++8v5 ca-certificates && \
    ln -sf /dev/stdout /var/log/rtorrent.log && \
    ln -sf /dev/stderr /var/log/rtorrent.log && \
    rm -rf /var/lib/apt/lists/*

COPY --from=builder /usr/local /usr/local

ENTRYPOINT ["/usr/local/bin/rtorrent"]
CMD ["-o", "import=/usr/local/etc/rtorrent/rtorrent.rc"]
