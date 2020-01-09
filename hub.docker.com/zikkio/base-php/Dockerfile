FROM php:7-fpm

RUN apt-get -y update && apt-get -y install git-core zip unzip libmcrypt-dev zlib1g-dev

RUN docker-php-ext-install mcrypt mbstring tokenizer pdo_mysql mysqli zip

COPY php.ini /usr/local/etc/php/

RUN usermod -u 1000 www-data

EXPOSE 9000
