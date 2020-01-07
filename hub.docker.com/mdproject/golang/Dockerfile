FROM golang:alpine

RUN apk add --no-cache git openssh

RUN go get -u golang.org/x/lint/golint

RUN cp /go/bin/golint /usr/local/go/bin

RUN rm -rf /go/bin /go/src