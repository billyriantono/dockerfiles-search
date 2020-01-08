FROM php:7.2.8-fpm-alpine

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN apk add --no-cache libxml2-dev curl-dev curl autoconf build-base freetype-dev libjpeg-turbo-dev libpng-dev freetype libpng libjpeg-turbo icu-dev && pecl install apcu \
&& docker-php-ext-enable apcu && docker-php-ext-install mysqli pdo_mysql mbstring xml dom curl zip gd intl \
&& docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/  --with-png-dir=/usr/include/  --with-jpeg-dir=/usr/include/ && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) &&  docker-php-ext-install -j${NPROC} gd \
&& apk del curl-dev libxml2-dev build-base autoconf && wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet && mv composer.phar /usr/bin/composer && apk del libxml2-dev curl-dev freetype-dev libjpeg-turbo-dev libpng-dev
