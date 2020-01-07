FROM alpine:3.3

MAINTAINER James Hall

RUN apk update \
  && apk add ca-certificates \
  && apk add python3 \
  && apk add python3-dev build-base libffi-dev openssl-dev --update-cache \
  && python3 -m ensurepip \
  && pip3 install --upgrade pip setuptools \
  && rm -rf /usr/lib/python*/ensurepip \
  && rm -rf /root/.cache \
  && rm -rf /var/cache/apk/*
