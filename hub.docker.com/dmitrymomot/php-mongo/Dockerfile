FROM php:fpm

RUN apt-get update && apt-get upgrade -y && apt-get install -y pkg-config libssl-dev \
    && pecl install mongodb \
    && pecl install xdebug \
    && docker-php-ext-enable mongodb xdebug
