FROM php:7.2-apache-stretch

# Install required PHP packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        libxml2-dev libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libzip-dev \
        zip \
        libexif-dev \
        graphicsmagick \
        ghostscript


# Configure PHP
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install -j$(nproc) mysqli soap gd zip opcache intl

COPY php.ini /usr/local/etc/php/conf.d/


# Configure Apache
RUN a2enmod rewrite && \
    a2enmod headers

COPY 000-default.conf /etc/apache2/sites-available/
COPY apache2.conf /etc/apache2/


# Cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/src/*
