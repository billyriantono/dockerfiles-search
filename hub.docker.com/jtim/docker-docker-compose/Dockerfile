# https://hub.docker.com/_/docker
# https://docs.docker.com/release-notes/
FROM docker:18.09.6-git

MAINTAINER tim@jtim.nl

ARG DOCKER_COMPOSE_VERSION=1.24.0

ENV USERNAME=bob-the-builder

RUN apk add --update \
    # https://wiki.alpinelinux.org/wiki/Docker#Docker_Compose
    py-pip sshpass openssh-client python-dev libffi-dev openssl-dev gcc libc-dev make && \
    pip install --no-cache-dir docker-compose==$DOCKER_COMPOSE_VERSION && \
    rm -rf /var/cache/apk/*

RUN addgroup -g 1000 -S ${USERNAME} && \
    adduser -u 1000 -S ${USERNAME} -G ${USERNAME}

USER ${USERNAME}