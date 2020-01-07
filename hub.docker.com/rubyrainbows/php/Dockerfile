FROM php:7.0-fpm-alpine

RUN apk upgrade --update && apk add --no-cache --virtual .build-deps \
        freetype-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \

        sqlite-dev \
        openssl-dev \
        curl-dev \
        libxml2-dev \
        ssmtp \
        icu-dev \
        autoconf \
        g++ \
        make \

    && docker-php-ext-install \
        iconv json mcrypt mbstring mysqli pdo_mysql pdo_sqlite phar curl ftp hash session simplexml tokenizer xml xmlrpc zip intl pcntl \
    && docker-php-ext-configure \
        gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
        gd \
