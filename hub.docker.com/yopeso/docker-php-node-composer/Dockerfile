FROM composer:latest AS composer
ENV COMPOSER_ALLOW_SUPERUSER 1

FROM php:7.1-apache

RUN apt update && apt -y install gnupg2 libmcrypt-dev mcrypt zlib1g-dev libpq-dev gettext-base && docker-php-ext-install mcrypt zip pdo_pgsql pgsql && docker-php-ext-enable mcrypt zip pdo_pgsql pgsql

RUN a2enmod rewrite

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

