FROM golang:alpine

MAINTAINER Dmitry Momot <mail@dmomot.com>

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh curl
    
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
    
WORKDIR "$GOPATH/src/app"
