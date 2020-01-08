ARG NODEJS_VERSION
FROM node:${NODEJS_VERSION:-10.14.0}-alpine

ARG NODEJS_VERSION
ENV NODEJS_VERSION=${NODEJS_VERSION:-10.14.0}

RUN apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/v3.8/main/ upgrade     && \
    apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/v3.8/main/ add            \
    python-dev libffi-dev openssl-dev build-base autoconf automake                             \
    sshpass openssh-client rsync bash git openssh curl                                      && \
    rm -rf /tmp/*
