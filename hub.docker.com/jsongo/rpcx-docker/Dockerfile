FROM golang:1.10-alpine3.7
LABEL maintainer "jsongo@qq.com"

ENV GOPATH /go

RUN apk update && apk add git
RUN go get -u -v -tags "consul quic" github.com/smallnest/rpcx/...
RUN go get github.com/rpcx-ecosystem/rpcx-examples3

VOLUME /go/src
WORKDIR /go/src
# ENTRYPOINT [ "go" ]
CMD ["go", "run", "/go/src/code/server.go"]
