FROM alpine:3.4

MAINTAINER coolchyni, coolchyni@gmail.com

RUN apk add --update-cache \
        python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    rm -r /root/.cache && \
    rm -rf /var/cache/apk/*
