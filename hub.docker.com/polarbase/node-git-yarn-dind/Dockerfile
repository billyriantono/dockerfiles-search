FROM mhart/alpine-node:12

ENV DOCKER_HOST tcp://docker:2375/
ENV DOCKER_DRIVER overlay

RUN apk add --no-cache docker git python make gcc g++ linux-headers binutils-gold gnupg libstdc++ libgcc
