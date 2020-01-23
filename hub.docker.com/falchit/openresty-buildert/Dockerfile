FROM php:7.1-apache

RUN docker-php-ext-install pdo_mysql
RUN a2enmod rewrite
RUN service apache2 restart

ADD . /var/www
ADD ./public /var/www/html

WORKDIR /var/www

RUN chown www-data:www-data -R storage