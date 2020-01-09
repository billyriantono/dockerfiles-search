FROM php:7.2.1-apache

# Enable Apache Rewrite module
RUN a2enmod rewrite

# Install PHP libraries
RUN apt-get update -y && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev

# Configure and install PHP extensions
RUN docker-php-ext-configure \
    gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ \
    && docker-php-ext-install \
    pdo_mysql \
    mysqli \
    gd \
    zip

# Install and enable PHP mcrypt
RUN pecl install \
    mcrypt-1.0.1 \
    && docker-php-ext-enable \
    mcrypt