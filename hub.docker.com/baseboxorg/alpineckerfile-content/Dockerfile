FROM debian:stretch-slim
MAINTAINER Chris Bartlett <bartlettc@gmail.com>

# Fluent Bit version
ENV FLB_VERSION 0.12.4

ENV FLB_TARBALL http://github.com/fluent/fluent-bit/archive/v$FLB_VERSION.zip

RUN mkdir -p /fluent-bit/bin /fluent-bit/etc /fluent-bit/log

RUN apt-get -qq update \
    && apt-get install -y -qq \
       ca-certificates \
       build-essential \
       cmake \
       make \
       sudo \
       wget \
       unzip \
       libsystemd-dev \
    && apt-get install -y -qq --reinstall lsb-base lsb-release \
    && wget -O "/tmp/fluent-bit-${FLB_VERSION}.zip" ${FLB_TARBALL} \
    && cd /tmp && unzip "fluent-bit-$FLB_VERSION.zip" \
    && cd "fluent-bit-$FLB_VERSION"/build/ \
    && cmake -DFLB_DEBUG=On -DFLB_TRACE=On -DFLB_JEMALLOC=On -DFLB_BUFFERING=On ../ \
    && make \
    && install bin/fluent-bit /fluent-bit/bin/ \
    && apt-get remove --purge --auto-remove -y -qq \
       build-essential \
       cmake \
       make \
       wget \
       unzip \
       libsystemd-dev \
    && rm -rf /tmp/*

# Configuration files
COPY config/fluent-bit.conf /fluent-bit/etc/
COPY config/parsers.conf /fluent-bit/etc/
COPY config/parsers_java.conf /fluent-bit/etc/

# Entry point
CMD ["/fluent-bit/bin/fluent-bit", "-c", "/fluent-bit/etc/fluent-bit.conf"]
