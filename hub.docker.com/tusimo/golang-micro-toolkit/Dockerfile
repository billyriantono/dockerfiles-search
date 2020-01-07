FROM golang:1.12-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk update && apk upgrade && \
    apk add --no-cache curl \
        wget \
        git \
        vim \
        protobuf \
        make
RUN go get -u github.com/golang/protobuf/protoc-gen-go && \
	go get -u github.com/micro/protoc-gen-micro
