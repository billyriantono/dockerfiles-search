FROM php:7.0-apache

RUN curl https://getcomposer.org/download/1.2.1/composer.phar > /usr/local/sbin/composer.phar > /usr/local/sbin/composer \
    && chmod +x /usr/local/sbin/composer

RUN apt-get update # @TODO Roll this into apt-get install and add clean up

RUN apt-get install -y \
    cron \
    git \
    libpng-dev \
    mysql-client \
    zip \
    zlib1g-dev

# Install required PHP extensions
RUN docker-php-ext-install \
    gd \
    pdo_mysql \
    sockets \
    zip

# Enable mod_rewrite
RUN a2enmod rewrite
