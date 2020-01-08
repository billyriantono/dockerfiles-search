FROM php:7.1-fpm-alpine

RUN apk update && apk add autoconf gcc build-base enchant-dev openssl-dev openssh git \
        && pecl install mongodb && docker-php-ext-enable mongodb \
        && (echo "\n" | pecl install apcu) && docker-php-ext-enable apcu \
        && docker-php-ext-install opcache

WORKDIR /var/www/html

