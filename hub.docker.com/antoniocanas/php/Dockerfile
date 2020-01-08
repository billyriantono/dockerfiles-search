FROM php:7.1-fpm-alpine
MAINTAINER Antonio Canas <antonio.canas.poblete@gmail.com>

ENV \
  BUILD_DEPS=' \
    # For xdebug
    autoconf \
  ' \

  PACKAGES=' \
    # For mcrypt
    libmcrypt-dev \
    # For postgres
    postgresql-dev \
  ' \

  PHP_EXTENSIONS=' \
    mbstring \
    mcrypt \

    # Databases
    pdo \
    pdo_mysql \
    mysqli \
    pdo_pgsql \
    pgsql \
  ' \

  PECL_INSTALL=' \
    xdebug \
  ' \

  PHP_ENABLE=' \
    xdebug \
  '

RUN \
  apk add --update --no-cache --virtual .build-deps \
    $PHPIZE_DEPS $BUILD_DEPS && \
  apk add --no-cache $PACKAGES && \
  docker-php-ext-install $PHP_EXTENSIONS && \
  pecl install $PECL_INSTALL && \
  docker-php-ext-enable $PHP_ENABLE && \

  # clean up
  apk del .build-deps && \
  rm -rf /tmp/*

ADD conf/ /usr/local/etc/php/conf.d/
