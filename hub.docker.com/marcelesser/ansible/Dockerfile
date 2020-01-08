FROM alpine:latest

RUN apk --update --no-cache add \
    docker \
    git \
    curl \
    wget \
    bash \
    sudo \
    python2 \
    py-boto \
    py2-cffi \
    py2-openssl \
    py2-pynacl \
    py2-paramiko \
    py2-yaml \
    py2-jinja2 \
    py2-docutils \
    py2-rsa \
    py2-dateutil \
    py2-futures

RUN apk --update --no-cache add py2-pip build-base python2-dev \
    && pip install ansible \
    && pip install awscli \
    && apk del py2-pip python2-dev build-base

