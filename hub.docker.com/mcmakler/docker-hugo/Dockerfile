FROM alpine:latest

MAINTAINER McMakler <admin@mcmakler.de>

# https://github.com/spf13/hugo/releases
ENV HUGO_VERSION=0.20.7

ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /tmp

RUN tar -xf /tmp/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /tmp \
    && mkdir -p /usr/local/sbin \
    && mv /tmp/hugo /usr/local/sbin/hugo \
    && rm -rf /tmp/hugo_${HUGO_VERSION}_linux_amd64

VOLUME /app

WORKDIR /app
