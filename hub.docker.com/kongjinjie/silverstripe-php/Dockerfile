FROM php:7.1.23-apache

RUN apt-get update -y && \
    apt-get install -y \
        zlib1g-dev \
        libpng-dev \
        libicu-dev \
        g++

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN docker-php-ext-install pdo_mysql && docker-php-ext-enable pdo_mysql
RUN docker-php-ext-install gd && docker-php-ext-enable gd
RUN docker-php-ext-install intl && docker-php-ext-enable intl

RUN mv /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
