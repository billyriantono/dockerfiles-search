# See https://github.com/docker-library/php/blob/master/7.1/fpm/Dockerfile
FROM php:7.2-fpm

RUN apt-get update && apt-get install -y librabbitmq-dev zip unzip git openssl

# Install extensions
RUN docker-php-ext-install pdo pdo_mysql opcache
RUN pecl install redis && docker-php-ext-enable redis
RUN pecl install amqp && docker-php-ext-enable amqp

ADD php.ini /usr/local/etc/php

WORKDIR /var/www/app
