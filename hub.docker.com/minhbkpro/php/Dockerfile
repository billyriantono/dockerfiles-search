FROM php:7.2-fpm

WORKDIR /usr/src/www

RUN rm /etc/apt/preferences.d/no-debian-php
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  zlib1g-dev \
  libicu-dev \
  libcairo2-dev \
  libjpeg-dev \
  libgif-dev \
  libpng-dev \
  libxml2-dev \
  g++ \
  php-soap \
  procps

RUN docker-php-ext-install \
  mysqli \
  pdo \
  pdo_mysql \
  intl \
  zip \
  gd \
  soap
