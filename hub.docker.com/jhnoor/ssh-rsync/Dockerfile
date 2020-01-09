FROM alpine:3.8

RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
    rsync \
    openssh-client \
    openvpn \
    zip \
    python3 \
    && rm -rf /var/cache/apk/*

ENV DOCKER_COMPOSE_VERSION 1.22.0
RUN pip3 install docker-compose==$DOCKER_COMPOSE_VERSION