FROM php:5.6-apache
MAINTAINER Nitra

# VOLUME ["/var/www/"]

RUN apt-get update \ 
    && apt-get install -y \
        zlib1g-dev \
        git \
    && pecl install APCu-4.0.11 \
    && docker-php-ext-enable apcu \
    && docker-php-ext-install zip pdo_mysql opcache 

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add php.ini 
COPY php.ini /usr/local/etc/php