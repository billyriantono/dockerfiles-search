FROM golang:alpine

RUN apk add --update curl git make zip \
 && curl -s -L https://raw.githubusercontent.com/golang/dep/master/install.sh | sh \
 && apk del --purge curl
