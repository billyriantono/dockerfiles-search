FROM alpine:latest

ENV DOCKER_VERSION 17.03.1-ce

RUN apk add --no-cache curl && \
    set -x && \
    curl -L -o /tmp/docker-${DOCKER_VERSION}.tgz https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz && \
    tar -xz -C /tmp -f /tmp/docker-${DOCKER_VERSION}.tgz && \
    mv /tmp/docker/* /usr/bin

