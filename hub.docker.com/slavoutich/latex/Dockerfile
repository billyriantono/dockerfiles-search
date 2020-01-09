FROM debian:stable
MAINTAINER Viacheslav Ostroukh <v.dev@ostroukh.me>
ENV DEBIAN_FRONTEND noninteractive
USER root
WORKDIR /root

RUN apt-get update -q \
    && apt-get install -qy --no-install-recommends \
        build-essential \
        curl \
        wget \
        libfontconfig1 \
        python \
        python-pygments \
        texlive-full \
    && rm -rf /var/lib/apt/lists/*
