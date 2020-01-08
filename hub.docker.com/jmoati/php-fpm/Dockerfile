FROM php:fpm-alpine
MAINTAINER Jacques Moati <jacques@moati.net>

RUN apk --update \
    add libzip-dev libjpeg-turbo-dev libpng-dev freetype-dev icu-dev  pcre-dev libtool rabbitmq-c-dev shadow imagemagick imagemagick-dev autoconf g++ make && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install iconv gd bcmath exif intl opcache pcntl sockets zip pdo_mysql calendar mysqli && \
    pecl install imagick redis amqp && \
    docker-php-ext-enable imagick amqp redis && \
    rm -rf /tmp/* && \
    apk del --purge autoconf g++ libtool

COPY php.ini /usr/local/etc/php/

WORKDIR /app
