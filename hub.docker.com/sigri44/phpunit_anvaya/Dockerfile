FROM php:7.3.12
# Config Yarn apt
RUN apt-get update && apt-get install -y gnupg2
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update -yqq && apt-get install -y \
  apt-utils \
  git \
  libzip-dev \
  libcurl4-gnutls-dev \
  libicu-dev \
  libmcrypt-dev \
  libxml2-dev \
  libpng-dev \
  libbz2-dev -yqq \
  acl \
  yarn
RUN docker-php-ext-install mbstring pdo_mysql curl json intl gd xml zip bz2 opcache
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
