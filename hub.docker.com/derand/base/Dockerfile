FROM alpine:3.4
MAINTAINER derand

RUN apk update && \
    apk add tzdata && \
    cp /usr/share/zoneinfo/Europe/Kiev /etc/localtime
