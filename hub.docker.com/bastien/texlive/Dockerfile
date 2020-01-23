FROM debian:unstable

LABEL maintainer="bastien@silence.im"

RUN apt update && \
    apt dist-upgrade -y && \
    apt install -y texlive-full make && \
    rm -rf /var/lib/apt/lists/*
