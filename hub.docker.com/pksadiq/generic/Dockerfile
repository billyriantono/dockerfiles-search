FROM alpine:edge

RUN apk add --no-cache gcc musl-dev ccache meson gcovr && \
    wget https://github.com/ebassi/mutest/archive/master.tar.gz -O /master.tar.gz && \
    tar x -f /master.tar.gz && \
    meson mutest-master build --prefix=/usr && ninja -C build install && \
    rm -rf /master.tar.gz /mutest-master /build
