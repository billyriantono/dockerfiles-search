FROM python:3.6-alpine

RUN apk add --update --no-cache build-base openssl-dev libffi-dev git openssh \
    && pip install Fabric3 fabric3-virtualenv \
    && apk del build-base \
    && mkdir -p /data

WORKDIR /data
