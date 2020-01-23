FROM php:7.0-apache

ADD . /var/www/html

RUN docker-php-ext-install mysqli \
&& docker-php-ext-enable mysqli
