FROM php:7-fpm
MAINTAINER Thom Wiggers <thom@thomwiggers.nl>

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv gd

COPY resources/php.ini /usr/local/etc/php/php.ini

COPY resources/auththalia2 /usr/src/auththalia2

COPY resources/copy_auth.sh /usr/local/bin/copy_auth.sh
RUN chmod +x /usr/local/bin/copy_auth.sh
