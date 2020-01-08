FROM ubuntu:xenial

LABEL maintainer Zafar Iqbal <zafar@truemeridian.com>

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    openjdk-8-jre-headless \
    ca-certificates-java \
 && /var/lib/dpkg/info/ca-certificates-java.postinst configure \
 && rm -rf /var/lib/apt/lists/*
