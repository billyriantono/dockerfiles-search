FROM php:7.0-fpm

MAINTAINER Chaoyi Lu <iyoahcul@gmail.com>

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libmemcached-dev \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng12-dev \
        libfreetype6-dev \
        libssl-dev \
        libmcrypt-dev

#####################################
# Install The PHP Extention:
#####################################
RUN docker-php-ext-install mcrypt

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install bcmath
# RUN docker-php-ext-install pdo_pgsql

#####################################
# Install The PHP GD Library
#####################################
RUN docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd
