FROM golang:alpine

RUN apk update; \
    apk upgrade; \
    apk add --no-cache protobuf-dev git;

RUN go get -v github.com/golang/protobuf/protoc-gen-go

ENTRYPOINT [ "protoc" ]

WORKDIR /opt/mnt