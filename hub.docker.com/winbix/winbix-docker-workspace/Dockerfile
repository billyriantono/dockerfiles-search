FROM php:7.2-cli-alpine

RUN apk add --update icu curl libpng libjpeg freetype \
    nodejs nodejs-npm yarn python py-pip \
    jpeg-dev libpng-dev freetype-dev libzip-dev && \
    apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    zlib-dev icu-dev g++ libmemcached-dev jpeg-dev \
    libpng-dev freetype-dev openssl-dev libmcrypt-dev curl \
    # mycli build dependencies
    python-dev libffi-dev openssl-dev && \
    #
    docker-php-ext-configure zip \
        --with-libzip && \
    docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install -j$(nproc) pdo_mysql && \
    docker-php-ext-install -j$(nproc) zip && \
    docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-install bcmath && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl && \
    docker-php-ext-enable intl && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    #
    pip install mycli && \
    #
    apk del .build-deps

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN curl --insecure https://getcomposer.org/composer.phar \
    -o /usr/bin/composer && \
    chmod +x /usr/bin/composer && \
    composer global require hirak/prestissimo

WORKDIR /var/www/symfony

