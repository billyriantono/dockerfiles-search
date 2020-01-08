#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM php:7.2-fpm

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
# Installing tools and PHP extentions using "apt", "docker-php", "pecl",

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    curl \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
  && rm -rf /var/lib/apt/lists/*

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql \
  && docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd

#####################################
# SOAP:
#####################################

RUN rm /etc/apt/preferences.d/no-debian-php && \
    apt-get update -yqq && \
    apt-get -y install libxml2-dev php-soap && \
    docker-php-ext-install soap

#####################################
# PHP REDIS EXTENSION FOR PHP 7.x
#####################################

RUN printf "\n" | pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

#####################################
# ZipArchive:
#####################################

RUN docker-php-ext-install zip

#####################################
# bcmath:
#####################################

RUN docker-php-ext-install bcmath

#####################################
# Exif:
#####################################

RUN docker-php-ext-install exif

#####################################
# Opcache:
#####################################

RUN docker-php-ext-install opcache

#####################################
# Mysqli Modifications:
#####################################

RUN docker-php-ext-install mysqli

#####################################
# Tokenizer Modifications:
#####################################

RUN docker-php-ext-install tokenizer

#####################################
# Human Language and Character Encoding Support:
#####################################

RUN apt-get update -yqq && \
    apt-get install -y zlib1g-dev libicu-dev g++ && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl

#####################################
# Xdebug:
#####################################

RUN pecl install xdebug-2.6.1
RUN docker-php-ext-enable xdebug

#####################################
# Image optimizers:
#####################################

USER root

RUN apt-get update -yqq && apt-get install -y --force-yes jpegoptim optipng pngquant gifsicle

RUN apt-get update -y && \
    apt-get install -y libmagickwand-dev imagemagick && \
    pecl install imagick && \
    docker-php-ext-enable imagick

#####################################
# Python
#####################################
RUN apt-get install -y python-pip python-dev build-essential
RUN pip install --upgrade pip
RUN pip install --upgrade virtualenv
RUN pip install boto3==1.4.7

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#
# Clean up

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
