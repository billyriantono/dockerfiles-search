FROM php:5.6-apache

RUN apt-get update
RUN apt-get install -y mc vim mysql-client libpng12-dev imagemagick
RUN docker-php-ext-install mysql mysqli pdo pdo_mysql gd
RUN a2enmod rewrite

