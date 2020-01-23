FROM php:7.2-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && apk del --no-cache --purge .build-deps \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require "symfony/flex" --prefer-dist --no-progress --no-suggest --classmap-authoritative