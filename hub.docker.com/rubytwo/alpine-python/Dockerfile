FROM connorpoole/alpine-base:1.0.0

MAINTAINER Matt Rabinovitch <rabinovitchmatt@gmail.com>

RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    rm -r /root/.cache