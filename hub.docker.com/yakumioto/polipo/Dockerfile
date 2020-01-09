FROM alpine:latest

LABEL maintainer="yakumioto <yaku.mioto@gmail.com>"

RUN set -ex \
    && echo http://dl-cdn.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories \
    && apk update \
    && apk add --no-cache polipo

