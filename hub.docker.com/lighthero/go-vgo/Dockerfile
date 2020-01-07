FROM golang:1.10-alpine

RUN apk add --update --no-cache bash build-base git && rm -rf /var/cache/apk/*

RUN go get -u golang.org/x/vgo
RUN vgo version

ENV IS_DOCKER true
