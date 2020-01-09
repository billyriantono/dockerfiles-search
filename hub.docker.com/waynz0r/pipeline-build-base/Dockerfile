FROM golang:1.11-alpine

RUN apk add --update --no-cache bash ca-certificates curl git make

RUN mkdir -p /go/src/github.com/banzaicloud
WORKDIR /go/src/github.com/banzaicloud

RUN git clone https://github.com/banzaicloud/pipeline
WORKDIR /go/src/github.com/banzaicloud/pipeline

RUN make vendor
