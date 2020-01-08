# Common base image for a PHP 7.3.2 environment with MySQL, Redis and some other required core libraries
FROM php:7.3.2-fpm

ARG DEBIAN_FRONTEND=noninteractive

# 2019-05-09/JSt the duplicated update command is required, since the first call 
# currently fails, due to a removed package in the debian base imaged
RUN apt-get update --fix-missing && \
    apt-get autoremove && \
    apt-get install -y apt-utils && \
    apt-get upgrade -y
RUN apt-get install -y \
    curl  \
    zlib1g-dev \
    libzip-dev

RUN pecl channel-update pecl.php.net
RUN docker-php-ext-install zip opcache

RUN pecl install redis && docker-php-ext-enable redis
RUN docker-php-ext-install pdo pdo_mysql mysqli pcntl

RUN apt-get clean

WORKDIR /var/www/html

EXPOSE 80
