FROM alpine:latest
MAINTAINER K Jarrett <kj@kingj.net>

RUN apk update
RUN apk upgrade
RUN apk add nsd

VOLUME /zones /etc/nsd
EXPOSE 53 53/udp