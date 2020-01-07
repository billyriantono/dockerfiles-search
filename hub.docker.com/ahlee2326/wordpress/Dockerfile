FROM wordpress:php7.1-fpm-alpine

ENV APCU_VERSION 5.1.8

RUN set -xe \
    && apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        zlib-dev \
    && pecl install \
        apcu-$APCU_VERSION \
    && docker-php-ext-install \
        zip \
    && docker-php-ext-enable --ini-name 20-apcu.ini \
        apcu \
    && apk del .build-deps
