FROM composer/composer

FROM php:7.3-alpine

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN composer global require hirak/prestissimo

RUN set -xe \
    && apk add --no-cache --virtual .persistent-deps zlib-dev libzip-dev git unzip \
    && docker-php-ext-install zip
