FROM golang:1.6-alpine

RUN apk add --update git && \
    export GOPATH=/usr/local && \
    go get github.com/tools/godep && \
    go get github.com/go-ini/ini && \
    go get github.com/jmespath/go-jmespath && \
    export GOPATH=/go

WORKDIR /go/bin

CMD ["go"]