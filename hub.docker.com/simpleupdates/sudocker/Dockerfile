FROM php:7.2-apache

# Much inspiration derived from oopartners/php
# https://hub.docker.com/r/oopartners/php/~/dockerfile/

# gnupg required for running the curl commands in CircleCI
RUN apt-get update && apt-get install -y --no-install-recommends gnupg apt-utils

RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/local/bin
RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -

# default-libmysqlclient-dev: Allows use of mysql_config_editor cli
# libpng-dev: For CircleCI, either QUnit or Sinon...
# sendmail: To enable SUFramework to send email from inside Docker
RUN apt-get update && apt-get install -y --no-install-recommends \
  autoconf \
  default-libmysqlclient-dev \
  gettext \
  libbz2-dev \
  libcurl4-openssl-dev \
  libexif-dev \
  libgd-dev \
  libicu-dev \
  libkrb5-dev \
  libldap2-dev \
  libmagickwand-dev \
  libpng-dev \
  libssl-dev \
  libxml2-dev \
  mysql-client \
  nodejs \
  openssl \
  sendmail \
  ssh \
  sudo \
  unzip \
  wget \
  zlib1g-dev \
  && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/git/git/archive/v2.10.0.tar.gz && \
  tar xzvf v2.10.0.tar.gz && \
  cd git-2.10.0/ && \
  make configure && \
  ./configure --prefix=/usr && \
  make all && \
  make install

RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-png-dir=/usr
RUN docker-php-ext-configure bcmath
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/

RUN docker-php-ext-install \
  intl \
  dom \
  gd \
  exif \
  mysqli \
  pdo \
  pdo_mysql \
  gettext \
  mbstring \
  soap \
  ftp \
  bcmath \
  curl \
  bz2 \
  calendar \
  sockets \
  ldap \
  zip

RUN a2enmod rewrite

RUN pecl install imagick && docker-php-ext-enable imagick

RUN yes | pecl install xdebug

# phplint: for checking code style during CircleCI testing

RUN npm install -g \
	less \
	less-plugin-clean-css \
	bower \
	phplint \
	svgo \
	svg-bounding-box \
	qunit

RUN curl -sS https://getcomposer.org/installer | \
  php -- --install-dir=/usr/local/bin --filename=composer && \
  composer global require "hirak/prestissimo:^0.3"
