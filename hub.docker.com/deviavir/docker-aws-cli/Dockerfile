FROM alpine:3.5

MAINTAINER Chase Sillevis <chase@sillevis.net>

RUN apk --update add \
    python \
    py-pip \
    jq \
    && pip install awscli \
    && apk del py-pip \
    && rm -rf /var/cache/apk/*

