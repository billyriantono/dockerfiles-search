FROM ubuntu:xenial

MAINTAINER André Formento <andreformento.sc@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -q \
    && apt-get install -qy \
                       texlive-full \
                       python-pygments gnuplot \
                       pandoc abiword \
                       make git \
    && update-texmf \
    && texhash \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /data

VOLUME ["/data"]
