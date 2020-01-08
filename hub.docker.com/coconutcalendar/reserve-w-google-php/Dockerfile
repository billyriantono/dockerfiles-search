FROM php:7.4-fpm-alpine

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN apk add --no-cache autoconf g++ make \
    && yes '' | pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-install opcache pcntl pdo pdo_mysql \
    && mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini" \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted gnu-libiconv \
    && apk del --purge autoconf g++ make

ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

COPY config.ini "$PHP_INI_DIR/conf.d/"
COPY miscellaneous.ini "$PHP_INI_DIR/conf.d/"
COPY opcache.ini "$PHP_INI_DIR/conf.d/"
