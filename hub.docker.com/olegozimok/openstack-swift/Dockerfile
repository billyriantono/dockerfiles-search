FROM alpine:latest

MAINTAINER "Oleh Ozimok" <ozimok.oleg@gmail.com>

RUN apk add --update --no-cache python py-pip python-dev openssl build-base linux-headers ca-certificates \
    && pip install python-swiftclient python-keystoneclient

ENTRYPOINT ["/usr/bin/swift"]
