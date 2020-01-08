FROM php:5.6-apache

MAINTAINER Per Persson <per.persson@exertisztorm.com>

# Activate mod_rewrite
RUN a2enmod rewrite

# Install PHP zip module
RUN pecl install zip && echo "extension=zip.so" >> /usr/local/lib/php.ini

# Install PHP modules
RUN docker-php-ext-install pdo_mysql


# Install git
RUN apt-get update
RUN apt-get install -q -y git

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar && mv composer.phar /usr/local/bin/composer




# Copy source code into new image
ONBUILD COPY . /var/www

# Run composer
ONBUILD RUN composer --working-dir=/var/www install
