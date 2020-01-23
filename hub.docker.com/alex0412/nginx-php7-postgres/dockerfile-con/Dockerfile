FROM php:7.0-apache
MAINTAINER Alexander Pankov <ap@wdevs.ru>

ARG uid=1000
ARG gid=1000

RUN apt-get -qq update && apt-get upgrade -y && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libicu-dev \
    wget \
    nano \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo pdo_mysql intl \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install redis-3.1.0 && pecl install xdebug-2.5.0 \
    && docker-php-ext-enable redis xdebug

COPY config/php.ini /usr/local/etc/php
COPY config/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY config/apache2/ /etc/apache2/
RUN a2enmod rewrite

RUN groupadd -g $gid deploy && useradd -M -u $uid -g $gid deploy \
    && chown -R deploy /var/www/html

