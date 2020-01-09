FROM python:3-alpine3.8

RUN apk update && apk add --no-cache \
    zip \
    unzip \
    && rm -rf /var/cache/*

RUN pip3 install awscli
