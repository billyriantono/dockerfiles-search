FROM golang:1.12-alpine

RUN apk --no-cache add \
    bash \
    git \
    g++ \
    openssl

ENV HTTP_PROXY="http://172.30.65.47:8080"
ENV HTTPS_PROXY="http://172.30.65.47:8080"
ENV HTTP_PROXY_AUTH="basic:*:z00238418:Golang1.12.4"

