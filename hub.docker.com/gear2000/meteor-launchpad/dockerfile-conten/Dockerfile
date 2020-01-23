FROM php:7.3-cli-alpine3.9

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories
RUN sed -i 's/http/https/' /etc/apk/repositories

RUN mkdir -p /var/www/html

RUN apk add --no-cache --virtual .gc-build-deps m4 autoconf make gcc g++
RUN apk add --no-cache linux-headers openssl-dev nghttp2-dev
RUN apk add --no-cache hiredis-dev postgresql-dev

RUN docker-php-ext-install sockets

# For swoole 4.3.3
RUN printf "yes \n yes \n yes \n yes \n yes \n" | pecl install swoole

RUN docker-php-ext-enable sockets swoole

ENV PHP_INI_DIR /usr/local/etc/php
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

WORKDIR /var/www/html

RUN apk add --no-cache bash

RUN docker-php-source delete
RUN rm -rf /tmp/pear
RUN apk del .gc-build-deps

# EXPOSE 80
EXPOSE 9501
EXPOSE 9502
EXPOSE 9503
EXPOSE 9504
EXPOSE 9505


CMD ["php", "-a"]
