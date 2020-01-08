FROM golang:1.12.7-alpine

RUN set -ex && \
    apk add --no-cache \
    git \
    build-base \
    tar \
    gzip \
    curl

ENV GOPATH /go
ENV GLIDE_VERSION 0.13.3

RUN set -ex && \
    wget https://github.com/Masterminds/glide/releases/download/v${GLIDE_VERSION}/glide-v${GLIDE_VERSION}-linux-amd64.tar.gz && \
    tar -xvf  glide-v${GLIDE_VERSION}-linux-amd64.tar.gz && \
    mv linux-amd64/glide /usr/local/bin/glide && \
    rm -rf linux-amd64 && \
    rm glide-v${GLIDE_VERSION}-linux-amd64.tar.gz && \
    go get bitbucket.org/liamstask/goose/cmd/goose && \
    go get -u github.com/jessevdk/go-assets  && \
    go get -u github.com/jessevdk/go-assets-builder && \
    rm -rf /go/src
