FROM golang:alpine
MAINTAINER cblomart@gmail.com

RUN apk add --update --no-cache git mercurial gcc musl-dev upx docker
RUN go get github.com/alecthomas/gometalinter; \
    go get github.com/GeertJohan/go.rice/rice; \
    gometalinter --install; \
    mv /go/bin/* /usr/local/go/bin/; \
    rm -rf /go/*
