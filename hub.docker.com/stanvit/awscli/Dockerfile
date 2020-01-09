FROM alpine:3.6

MAINTAINER Stanislav Vitkovskiy <stas.vitkovsky@gmail.com>

RUN apk -U --no-cache add python2 py2-pip && \
    pip install awscli && \
    apk del py2-pip && \
    rm -rf /var/cache/apk/* /tmp/*
