# usage: https://github.com/hanguofeng/gocaptcha/wiki/QuickStartGocaptchaServer
FROM golang:alpine

ENV GOPATH=/go

RUN apk add --no-cache git \
	&& go get github.com/hanguofeng/gocaptcha/samples/gocaptcha-server \
	&& apk del git	

WORKDIR $GOPATH/src/github.com/hanguofeng/gocaptcha/samples/gocaptcha-server

EXPOSE 80

CMD $GOPATH/bin/gocaptcha-server -c gocaptcha.conf