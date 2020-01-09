FROM debian:jessie-slim
LABEL maintainer "zcsevcik@gmail.com"

RUN echo 'deb http://deb.debian.org/debian jessie-backports main' > /etc/apt/sources.list.d/backports.list && \

    apt-get update && \

    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    build-essential \
    gcc \
    g++ \
    gdb \
    gdbserver \
    make \
    pkg-config \
    make \
    gcovr \
    && \

    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y -t jessie-backports \
    cmake \
    && \

    rm -rf /var/lib/apt/lists/*
