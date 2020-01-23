FROM php:5.6-fpm

WORKDIR /app

RUN apt-get update
RUN apt-get install -y \
  git \
  zlib1g-dev \
  libpng12-dev \
  libjpeg62-turbo-dev \
  libfreetype6-dev \
  libmcrypt-dev \
  zip \
  npm

RUN docker-php-ext-install -j$(nproc) iconv mcrypt \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install \
  mbstring \
  zip \
  pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN npm install -g bower