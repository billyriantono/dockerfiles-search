FROM mhart/alpine-node:6

MAINTAINER Stas Alekseev <me@salekseev.com>

RUN apk add --no-cache --virtual .build-deps \
      git \
      python \
      gcc \
      g++ \
      make \
 && apk add --no-cache \
      avahi \
      avahi-compat-libdns_sd \
      avahi-dev \
      avahi-tools \
 && npm install -g --unsafe-perm homebridge homebridge-vera \
 && apk del .build-deps
