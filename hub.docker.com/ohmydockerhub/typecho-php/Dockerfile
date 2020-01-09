FROM php:fpm-alpine

MAINTAINER MrGeneral <mrgeneralgoo@gmail.com>

WORKDIR /www

# install depends
RUN apk add --no-cache libzip-dev freetype-dev libpng-dev libjpeg-turbo-dev \
    # install core extensions
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure zip \
    && docker-php-ext-install -j"$(getconf _NPROCESSORS_ONLN)" pdo_mysql zip \
    # clean
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*
