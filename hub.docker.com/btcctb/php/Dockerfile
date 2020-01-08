FROM php:7.0-apache

RUN apt-get update \
 && apt-get install -y git g++

# Composer
RUN curl -sS https://getcomposer.org/installer \
  | php -- --install-dir=/usr/local/bin --filename=composer

# pour ext ldap
RUN apt-get install -y libldap2-dev \
 && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
 && docker-php-ext-install ldap

# pour ext curl
RUN apt-get install -y libcurl4-openssl-dev \
 && docker-php-ext-install curl

# pour ext zip
RUN apt-get install -y zlib1g-dev \
 && docker-php-ext-install zip

# pour ext mysql/mariadb
RUN docker-php-ext-install mysqli pdo_mysql

# pour ext xml
RUN apt-get install -y  libxml2-dev libxslt-dev \
 && docker-php-ext-install dom xmlrpc xsl

# pour ext webservices
RUN docker-php-ext-install gettext mbstring soap

# pour ext xdebug
RUN pecl install xdebug \
 && docker-php-ext-enable xdebug

# pour mods rewrite
RUN a2enmod rewrite \
 && a2enmod alias

# Configure php.ini
RUN echo "date.timezone = 'Europe/Brussels'" > /usr/local/etc/php/php.ini
RUN echo "short_open_tag = Off" >> /usr/local/etc/php/php.ini

WORKDIR /var/www/html
