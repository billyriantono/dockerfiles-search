FROM php:7.3-apache

#Install some common tools and postgres
RUN apt-get -qq update \
    && apt-get -qq -y install sudo \
    && apt-get -qq -y install multitail \
    && apt-get -qq -y install git \
    && apt-get -qq -y install wget \
    && apt-get -qq -y install zip \
    && apt-get -qq -y install unzip \
    && apt-get -qq -y install software-properties-common \
    && apt-get -qq -y install libpq-dev \
    && apt-get -qq -y install vim \
    && apt-get -qq -y install postgresql-client \
    && apt-get -qq -y install cron

RUN service cron start

# Install gdlib
RUN apt-get -qq -y install libpng++-dev libjpeg-dev libvpx-dev zlib1g-dev libgd-dev libzip-dev

# Install curl
RUN  apt-get -qq -y install libcurl4-gnutls-dev curl

#Install php-ldap
RUN     apt-get install libldap2-dev -y \
&&      docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
&&      docker-php-ext-install ldap

RUN docker-php-ext-configure zip --with-libzip
#Install other needed php extensions
RUN docker-php-ext-install pdo pdo_pgsql
RUN docker-php-ext-install json gd curl zip

#Install php-xdebug
RUN apt-get -qq update \
&& apt-get install -qq -y dh-php \
&& pecl install xdebug \
&& docker-php-ext-enable xdebug

#Install locales
RUN apt-get install -qq -y locales \
&& locale-gen de_DE \
&& locale-gen de_DE.UTF-8 \
&& update-locale

#Configure php.ini
COPY configure_xdebug.sh /home/configure_xdebug.sh
RUN chown root /home/configure_xdebug.sh
RUN chmod 770  /home/configure_xdebug.sh

RUN a2enmod rewrite

# workaround to use regular php version in cronjobs
RUN ln -s /usr/local/bin/php /usr/bin/php

WORKDIR /var/www

COPY base_php.ini /usr/local/etc/php/conf.d/base_php.ini
RUN mkdir /usr/local/etc/php/apache2
RUN cp -r /usr/local/etc/php/conf.d /usr/local/etc/php/apache2/conf.d
COPY apache_php.ini /usr/local/etc/php/apache2/conf.d/apache_php.ini
RUN echo 'export PHP_INI_SCAN_DIR=/usr/local/etc/php/apache2/conf.d' >> /etc/apache2/envvars
