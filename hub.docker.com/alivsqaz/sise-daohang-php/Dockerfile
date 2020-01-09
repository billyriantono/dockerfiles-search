FROM php:7.1-fpm-jessie
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        vim \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install mysqli
