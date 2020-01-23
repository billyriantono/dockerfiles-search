# Copyright (c) 2018 Arista Networks, Inc.  All rights reserved.
# Arista Networks, Inc. Confidential and Proprietary.

FROM golang:1.12.7-alpine3.10 as build
LABEL maintainer="fabrice@arista.com"

ENV VERSION 1.0.2

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

RUN apk add --no-cache \
    make=4.2.1-r2 \
    git=2.22.0-r0 \
    && wget https://github.com/jfrabaute/zookeeper_exporter/archive/${VERSION}.tar.gz \
    && echo "d0a57a24d9eaa7ae8c66d407f4fb32a591cff0480a39cd200a75a4221a6f9913b411df35628f5dccb9c6aa21c6f51011aebb6b245f8e55b049ca6c4eef5b93f3  ${VERSION}.tar.gz" | sha512sum -c - \
    && tar xvf ${VERSION}.tar.gz \
    && mkdir -p /go/src/github.com/jfrabaute/ \
    && mv zookeeper_exporter-${VERSION} /go/src/github.com/jfrabaute/zookeeper_exporter \
    && cd /go/src/github.com/jfrabaute/zookeeper_exporter \
    && GO_VERSION=1.12.7 make

FROM aristanetworks/base:3.9.3
LABEL maintainer="fabrice@arista.com"

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# Install binary
COPY --from=build /go/src/github.com/jfrabaute/zookeeper_exporter /usr/bin

ENTRYPOINT ["/usr/bin/dumb-init", "--", "/usr/bin/zookeeper_exporter"]
