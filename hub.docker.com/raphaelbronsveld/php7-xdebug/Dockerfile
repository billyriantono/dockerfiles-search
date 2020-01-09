FROM php:7.0-fpm-alpine
MAINTAINER Raphaël Bronvseld <raphaelbronsveld@outlook.com>

RUN apk update \
    && apk add  --no-cache g++ make autoconf \
    && docker-php-source extract \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-source delete \
    && rm -rf /tmp/*

COPY ./conf/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
