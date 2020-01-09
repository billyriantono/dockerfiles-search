FROM golang:1.11.4-alpine3.7

RUN apk add --no-cache \
        git \
        protobuf \
        build-base \
        openssh \
        tar \
        gzip \
        ca-certificates

RUN go get -u github.com/golang/protobuf/protoc-gen-go
