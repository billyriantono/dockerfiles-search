FROM alpine:3.6

MAINTAINER jsongo <jsongo@qq.com>

WORKDIR /src

RUN apk add --update go
RUN apk add --update git

RUN mkdir -p /go/src

ENV GOPATH /go
ENV PATH $PATH:$GOPATH/bin

RUN go get google.golang.org/grpc

RUN apk del git

ENTRYPOINT ["go"]
