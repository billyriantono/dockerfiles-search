FROM php:7.3-fpm-alpine

RUN apk add --no-cache libzip-dev freetype-dev libjpeg-turbo-dev libpng-dev icu-dev

RUN docker-php-ext-configure zip --with-libzip=/usr/include
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-configure intl

RUN docker-php-ext-install zip gd pdo pdo_mysql intl opcache

RUN apk add --no-cache wkhtmltopdf
