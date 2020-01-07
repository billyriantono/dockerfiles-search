FROM php:7.3-apache

RUN mkdir /var/www/cache \
    && chown www-data:www-data /var/www/cache \
    && a2enmod rewrite

COPY www/ /var/www/html
COPY config.docker.php /var/www/config.php
