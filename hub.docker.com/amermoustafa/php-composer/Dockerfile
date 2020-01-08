
ARG PHPVERSION=7.0

FROM webdevops/php:$PHPVERSION

FROM php:7.0-fpm-alpine as builder

RUN apk add --no-cache bzip2-dev coreutils sqlite-dev libxml2-dev curl-dev gmp-dev icu-dev libpng-dev jpeg-dev freetype-dev autoconf imagemagick-dev gcc libc-dev rabbitmq-c-dev make libtool \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/freetype2 --with-jpeg-dir=/usr/include \
        && docker-php-ext-install -j$(nproc) bcmath pdo pdo_mysql pdo_sqlite mbstring json xml zip curl gmp intl \
            gd soap sockets pcntl bz2 \
        && pecl install imagick \
        && pecl install amqp \
        && pecl install apcu \
        && docker-php-ext-enable imagick

FROM php:7.0-fpm-alpine

RUN apk add --no-cache bzip2-dev coreutils sqlite-dev libxml2-dev curl-dev gmp-dev icu-dev libpng-dev jpeg-dev freetype-dev autoconf imagemagick-dev gcc libc-dev rabbitmq-c-dev make libtool \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/freetype2 --with-jpeg-dir=/usr/include \
        && docker-php-ext-install -j$(nproc) bcmath pdo pdo_mysql pdo_sqlite mbstring json xml zip curl gmp intl \
            gd soap sockets pcntl bz2 \
        && pecl install imagick \
        && pecl install amqp \
        && pecl install apcu \
        && docker-php-ext-enable imagick

COPY composer /usr/bin/composer

RUN chmod 755 /usr/bin/composer

ENTRYPOINT [ "/usr/bin/composer" ]


