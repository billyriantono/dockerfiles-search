FROM copiousfreetime/base-alpine-s6-overlay:latest

LABEL maintainer="jeremy@dojo4.com"

RUN apk add --no-cache nginx php5-cli php5-fpm

EXPOSE 80

COPY rootfs /

