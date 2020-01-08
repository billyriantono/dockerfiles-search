FROM esycat/ubuntu:latest

MAINTAINER "Eugene Janusov" <esycat@gmail.com>

ARG VERSION=6.x
ENV NPM_CONFIG_PREFIX /usr/local

RUN wget -qO- https://deb.nodesource.com/setup_${VERSION} | bash -

RUN apt-get update && \
    apt-get -yq --no-install-recommends install nodejs && \
    apt-get clean && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/archive/* /var/lib/apt/lists/*

RUN npm config set -g prefix $NPM_CONFIG_PREFIX

