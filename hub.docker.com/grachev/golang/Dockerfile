FROM golang:alpine

ENV GOPATH /go
ENV GOBIN=$GOPATH/bin\
    PATH=$PATH:$GOBIN

RUN apk add --no-cache git gcc g++ make openssl

ENTRYPOINT ["go"]
