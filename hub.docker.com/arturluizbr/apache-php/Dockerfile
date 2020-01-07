FROM php:5.6-apache
MAINTAINER arturluizbr

RUN docker-php-ext-install mysqli mysql mbstring \
    && a2enmod rewrite
