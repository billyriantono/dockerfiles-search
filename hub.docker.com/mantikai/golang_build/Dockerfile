FROM golang:1.13.1-buster

# Git and protobuf Compiler
RUN apt-get update; apt-get install -y git protobuf-compiler libprotobuf-dev

# Golang Protobuf Plugin
RUN go get github.com/golang/protobuf/protoc-gen-go

# We had problems with system DNS
ENV GODEBUG=netdns=cgo

# Working directory outside of GOPATH (which is /go)
RUN mkdir /work
WORKDIR /work
