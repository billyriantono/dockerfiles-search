FROM php:5.6-apache

MAINTAINER Jason Webb jason@jswebb.net

RUN a2enmod rewrite
RUN a2enmod ssl

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        php5-memcached \
        php5-mysql \
    && docker-php-ext-install iconv mcrypt mysqli pdo pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mbstring