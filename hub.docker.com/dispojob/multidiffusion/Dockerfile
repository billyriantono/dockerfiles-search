FROM php:apache

ENV APACHE_DOCUMENT_ROOT /app/web
ENV APACHE_FALLBACK_RESOURCE /app.php

RUN apt-get update \
 && apt-get install -y libzip-dev unzip \
 && docker-php-ext-install pdo_mysql zip \
 && php -m

RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

COPY 000-default.conf /etc/apache2/sites-available/
COPY php.ini /usr/local/etc/php/

WORKDIR /app

