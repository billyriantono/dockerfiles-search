FROM php:5.4-apache
MAINTAINER outan "outannexway@gmail.com"

COPY php.ini /usr/local/etc/php/
RUN apt-get update && \
    docker-php-ext-install pdo_mysql mysqli mbstring &&\
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libmcrypt-dev vim
