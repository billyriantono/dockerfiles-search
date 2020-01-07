FROM alpine:3.2
MAINTAINER Yves Serrano <y@yas.ch>

RUN apk add --update \
        git \
        mercurial \
        autoconf \
        automake \
        libpng-dev \
        readline-dev \
        zlib-dev \
        jpeg-dev \
        g++ \
        gcc \
        libxml2-dev \
        libxslt-dev \
        sqlite \
        sqlite-dev \
        yaml-dev \
        libpng-dev \
    && rm -rf /var/cache/apk/*
