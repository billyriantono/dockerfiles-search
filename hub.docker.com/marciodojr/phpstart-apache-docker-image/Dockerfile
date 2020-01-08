FROM php:7.2.8-apache-stretch

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN apt-get update && apt-get install libxml2-dev libcurl4-gnutls-dev zlib1g-dev wget libpng-dev -y && pecl install apcu xdebug && docker-php-ext-enable apcu xdebug && docker-php-ext-install mysqli pdo_mysql mbstring xml dom curl zip gd && wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet && mv composer.phar /usr/bin/composer && apt-get purge libcurl4-gnutls-dev libxml2-dev zlib1g-dev wget -y && apt-get clean cache && a2enmod rewrite expires