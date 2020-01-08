FROM alpine:latest
MAINTAINER Jake Skeates <jskeates@me.com>

RUN apk add --update openvpn \
 && rm -rf /var/cache/*

VOLUME /etc/openvpn
EXPOSE 1194

