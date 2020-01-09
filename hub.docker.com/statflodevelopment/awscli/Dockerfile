FROM alpine:latest

ENV VERSION 1.10.61

RUN apk add --update \
    python \
    py-pip && \
    adduser -D aws

WORKDIR /home/aws

RUN mkdir aws && \
    pip install --upgrade -I pip && \
    pip install awscli==$VERSION

USER aws
