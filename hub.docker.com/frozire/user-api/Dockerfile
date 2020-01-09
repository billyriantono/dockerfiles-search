FROM php:7.1-fpm

RUN apt-get update

RUN apt-get install -y --no-install-recommends curl git zlib1g-dev

RUN docker-php-ext-install zip

RUN docker-php-ext-install pdo_mysql

RUN docker-php-ext-install json

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html
