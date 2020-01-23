#FROM alpine:3.5
FROM openjdk:8u111-jre-alpine

MAINTAINER John <yinzhuan@cisco.com>

ENV DISPLAY=:99 \
    FF_VERSION=45.6.0-r0 \
    LC_ALL=C

RUN  apk --no-cache add dbus fontconfig ttf-freefont xvfb firefox-esr=$FF_VERSION

ENTRYPOINT Xvfb :99  -screen 0 1920x1080x16 +extension RANDR   
