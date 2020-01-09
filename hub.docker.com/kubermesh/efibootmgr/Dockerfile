FROM debian:jessie
# Alpine doesn't have an efibootmgr package yet, see https://bugs.alpinelinux.org/issues/3819

RUN apt-get update && \
    apt-get install -y efibootmgr && \
    rm -rf /var/lib/apt/lists/*
