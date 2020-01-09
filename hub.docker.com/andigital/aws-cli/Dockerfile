FROM alpine:latest

MAINTAINER AND Digital <hello@and.digital>

RUN apk add --update --quiet python py-pip groff && \
    pip install awscli==1.11.131 && \
    rm -rf /var/cache/*
