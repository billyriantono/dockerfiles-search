FROM php:7.0-apache

RUN apt-get update \
    && apt-get install -y libmcrypt-dev libmemcached-dev libsqlite3-dev libcurl3-dev \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-configure curl \
    && docker-php-ext-configure pdo_sqlite
