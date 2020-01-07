FROM ubuntu:16.04

MAINTAINER Bitnami <containers@bitnami.com>

RUN apt-get update && \
    apt-get install -y git build-essential unzip file curl ca-certificates sudo locales procps libaio1 gnupg dirmngr && \
    update-locale LANG=C.UTF-8 LC_MESSAGES=POSIX && \
    locale-gen en_US.UTF-8

ENV NAMI_VERSION=1.0.0-1

RUN cd /tmp && \
    curl -sSLO https://nami-prod.s3.amazonaws.com/tools/nami/releases/nami-$NAMI_VERSION-linux-x64.tar.gz && \
    echo "80488279b056d5e9c183fe34097c5f496715ab16a602afcc9f78d59f15139a16  nami-$NAMI_VERSION-linux-x64.tar.gz" | sha256sum -c - && \
    mkdir -p /opt/bitnami/nami && \
    tar xzf nami-$NAMI_VERSION-linux-x64.tar.gz --strip 1 -C /opt/bitnami/nami && \
    rm nami-$NAMI_VERSION-linux-x64.tar.gz

ENV PATH=/opt/bitnami/nami/bin:$PATH

COPY rootfs /
