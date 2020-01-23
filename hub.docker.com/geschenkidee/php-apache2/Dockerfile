FROM php:7.0-apache

# Install developer dependencies
RUN apt-get update -yqq && apt-get install -y git wget libsqlite3-dev libxml2-dev libicu-dev libfreetype6-dev libmcrypt-dev libjpeg62-turbo-dev libpng12-dev git libcurl4-gnutls-dev libbz2-dev libssl-dev -yqq

### PAGESPEED ####
RUN wget https://dl-ssl.google.com/dl/linux/direct/mod-pagespeed-stable_current_amd64.deb
RUN dpkg -i mod-pagespeed-*.deb
RUN rm -f mod-pagespeed-*.deb
RUN apt-get -f install -y
RUN chown 999.999 /var/cache/mod_pagespeed
RUN chown 999.999 /var/log/pagespeed

# Install php extensions
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install xml
RUN docker-php-ext-install zip
RUN docker-php-ext-install bz2
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install curl

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

# Install PECL extensions
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN a2enmod rewrite
RUN a2enmod headers
RUN a2enmod expires