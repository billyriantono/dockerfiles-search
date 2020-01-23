FROM php:5-apache

RUN a2enmod rewrite
RUN docker-php-ext-install pdo_mysql

COPY ./php.ini /usr/local/etc/php/
