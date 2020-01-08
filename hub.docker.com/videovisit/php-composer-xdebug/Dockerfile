FROM composer:1.8.5

RUN apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS

RUN pecl install xdebug \
 && docker-php-ext-enable xdebug

