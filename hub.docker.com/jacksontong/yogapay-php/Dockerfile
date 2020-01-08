FROM php:7.3.8-cli-alpine

RUN apk add composer icu-dev zlib-dev gcc g++ libtool make autoconf \
    freetype-dev freetype libjpeg-turbo-dev libpng-dev libjpeg-turbo libpng \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j${NPROC} gd \
    && docker-php-ext-install bcmath