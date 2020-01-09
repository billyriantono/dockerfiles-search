FROM php:7.2-fpm-alpine

ENV BUILD_DEPS="autoconf g++ libtool make pcre-dev tzdata" \
    PHPREDIS_VERSION=3.1.2

RUN apk --update upgrade --no-cache; \
    apk add --no-cache --virtual .build-deps ${BUILD_DEPS}; \
    apk add --no-cache \
        libxml2-dev \
        libzip-dev

# Basic extensions
RUN docker-php-ext-install \
    opcache \
    zip \
    pdo \
    pdo_mysql \
    tokenizer \
    xml \
    ctype \
    json \
    bcmath

# Mcrypt
RUN apk add --no-cache --update libmcrypt-dev \
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt

# Redis
RUN docker-php-source extract \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && docker-php-source delete

# Imagick
RUN apk add --update --no-cache imagemagick-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# XDebug
RUN pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug

# Git & composer
RUN apk add --update --no-cache git; \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# Set UTC timezone
RUN cp /usr/share/zoneinfo/Etc/UTC /etc/localtime; \
    echo "UTC" | tee /etc/timezone

# Clean
RUN apk del .build-deps; \
    rm -rf /var/cache/apk/*

# Disable PHP exposing
# https://secure.php.net/manual/en/ini.core.php#ini.expose-php
RUN echo "expose_php=0" > /usr/local/etc/php/php.ini

RUN sed -i -e 's/listen.*/listen = 0.0.0.0:9000/' /usr/local/etc/php-fpm.conf

# Production
# RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

CMD ["php-fpm"]
