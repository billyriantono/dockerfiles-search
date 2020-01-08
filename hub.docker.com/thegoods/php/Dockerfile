FROM php:5.6.30-fpm-alpine
MAINTAINER Curt Puckett

RUN apk add --no-cache mysql-client curl bash redis imagemagick-dev

RUN apk add --no-cache libtool build-base autoconf libjpeg-turbo-dev libpng-dev \
        && pecl install imagick \
        && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini \
        && docker-php-ext-install gd mysqli opcache \
        && apk del libtool build-base autoconf