FROM golang:1.13-alpine as build

ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GOARCH=amd64

RUN \
    apk add --no-cache --update git && \
    go get -u github.com/golang/dep/cmd/dep && \
    go get -u github.com/stretchr/testify && \
    go get -u github.com/vektra/mockery/.../ && \
    go get -u gopkg.in/alecthomas/gometalinter.v2 && \
    ln -s /go/bin/gometalinter.v2 /go/bin/gometalinter && gometalinter --install --force && \
    rm -rf /var/cache/apk/*
