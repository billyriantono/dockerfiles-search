FROM golang:1.11.0-alpine3.8
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories &&\
  apk update &&\
  apk add curl git &&\
  go get -u github.com/golang/dep/cmd/dep
WORKDIR /go/src/github.com