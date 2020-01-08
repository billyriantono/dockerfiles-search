FROM php:7.1-cli

RUN apt-get update \
 && apt-get install unzip zip git zlib1g-dev make gcc libpng-dev gnupg -y --force-yes
 
RUN pecl install xdebug

RUN docker-php-ext-install -j$(nproc) zip pdo_mysql
RUN docker-php-ext-enable zip pdo_mysql xdebug
