FROM php:5.6-apache

ENV APACHE_DOCUMENT_ROOT /app/web
ENV APACHE_FALLBACK_RESOURCE /app.php

RUN apt-get update \
 && apt-get install -y libfreetype6-dev libicu-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev libxml2-dev libzip-dev unzip zlib1g-dev \
 && pecl update-channels \
 && pecl install apcu-4.0.11 redis \
 && docker-php-ext-enable apcu redis \
 && docker-php-ext-install bcmath ctype gd iconv intl mbstring opcache pcntl pdo_mysql soap xml zip

RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

COPY 000-default.conf /etc/apache2/sites-available/
COPY php.ini /usr/local/etc/php/

WORKDIR /app
