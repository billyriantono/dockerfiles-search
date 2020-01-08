FROM php:7.1-fpm

RUN docker-php-ext-install pdo pdo_mysql

# Install the PHP gd library
RUN apt-get update -y && apt-get install -y sendmail libpng-dev
RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev

RUN docker-php-ext-install mbstring
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
