FROM alpine:latest
MAINTAINER EzriCloud <docker@ezricloud.com>

RUN apk update

ENV SSL_CERTBOTPORT 8888

COPY tools/ /tools/

RUN tools/lets-encrypt/install-lets-encrypt.sh
