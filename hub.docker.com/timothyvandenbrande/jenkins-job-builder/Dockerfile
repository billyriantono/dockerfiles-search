FROM alpine:3.8

ENV VERSION 2.5.0

RUN apk add --no-cache python && apk add --no-cache py-pip && \
    pip install jenkins-job-builder==${VERSION} && \
    pip install yamllint
