FROM php:7.0-apache

MAINTAINER Nitra

ENV TERM xterm

RUN a2enmod rewrite

# Change apache virtual host
COPY default-virtual-host.conf /etc/apache2/sites-enabled/000-default.conf

RUN apt-get update \
    && apt-get install -y \
        git \
        zlib1g-dev \
        npm \
        nodejs-legacy

RUN npm install -g uglifycss

# For composer and zlib1g-dev also for this module
RUN docker-php-ext-install zip && \
    docker-php-ext-install pdo_mysql

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY php.ini /usr/local/etc/php
#Adding path to xdebug.so into xdebug configfile
RUN echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-$(pecl install xdebug-2.4.1 | grep -o -P '(?<=zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-).*(?=/xdebug.so)')$xdebugDirName/xdebug.so" >> /usr/local/etc/php/conf.d/xdebug.ini

# Install composer and Asset plugin for Bower dependencies management
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    composer global require "fxp/composer-asset-plugin:~1.2"

WORKDIR /var/www

CMD ["apache2-foreground"]