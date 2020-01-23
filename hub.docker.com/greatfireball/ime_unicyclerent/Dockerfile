FROM php:5.6-apache

RUN apt-get update && apt-get install -y \
    libxml2-dev \
    zlib1g-dev \
    zip unzip \
    git \
    && docker-php-ext-install -j$(nproc) mysql soap zip pdo_mysql

COPY php.ini /usr/local/etc/php/php.ini

RUN a2enmod rewrite

COPY get_composer.sh /usr/local/bin/get_composer.sh
RUN get_composer.sh && mv composer.phar /usr/local/bin/composer
