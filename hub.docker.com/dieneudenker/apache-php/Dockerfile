FROM php:7.1.29-apache-jessie

# Install system dependencies
RUN apt-get update
RUN apt-get -qq install libpng-dev libfreetype6-dev libjpeg-dev git zlib1g-dev libicu-dev g++

# Install  mysqli extension for PHP
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-configure intl
RUN docker-php-ext-install mysqli gd zip pdo_mysql intl

# Install xdebug
RUN pecl install xdebug-2.6.0 && docker-php-ext-enable xdebug

# Enable mod rewrite
RUN a2enmod rewrite

# Create self signed certificate
RUN openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt -subj "/C=DE/ST=Denial/L=Springfield/O=Dis/CN=www.example.com"

# Enable ssl
RUN sed -i 's/ssl-cert-snakeoil.pem/apache-selfsigned.crt/g' /etc/apache2/sites-available/*.conf
RUN sed -i 's/ssl-cert-snakeoil.key/apache-selfsigned.key/g' /etc/apache2/sites-available/*.conf
RUN a2enmod ssl && a2enmod headers && a2ensite default-ssl

# Set apache document root
ENV APACHE_DOCUMENT_ROOT /var/www/web
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Set locale to de_DE.UTF-8
RUN apt-get install -y locales locales-all
ENV LC_ALL de_DE.UTF-8
ENV LANG de_DE.UTF-8
ENV LANGUAGE de_DE.UTF-8

# Copy config file
COPY php.ini /usr/local/etc/php 

# Install ICU fo php
RUN apt-get -y install libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

# Add Xdebug to Zend Engine
RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/php.ini

# Set workdir
WORKDIR ${APACHE_DOCUMENT_ROOT}
