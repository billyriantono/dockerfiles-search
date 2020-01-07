FROM alpine:3.3

MAINTAINER Brett Fieber <brett.fieber@latch.com>

# Gets jdk8 from edge/testing branch
RUN apk add openjdk8-jre-base --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
    && rm -rf /var/cache/apk/*
