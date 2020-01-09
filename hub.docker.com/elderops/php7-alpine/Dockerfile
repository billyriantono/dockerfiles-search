FROM php:7-alpine
LABEL Matthew Ridehalgh <matthew.ridehalgh@elder-studios.co.uk>

RUN apk --update --no-cache add wget \
  curl \
  ca-certificates \
  openssl \
  php7-phar \
  php7-json \
  php7-iconv \
  php7-session \
  php7-tokenizer \
  php7-openssl \
  php7-soap \
  curl \
  git \
  grep \
  build-base \
  libmemcached-dev \
  libmcrypt-dev \
  libxml2-dev \
  zlib-dev \
  autoconf \
  cyrus-sasl-dev \
  libgsasl-dev \
  supervisor \
  && pecl install mcrypt-1.0.1 \
  && docker-php-ext-enable mcrypt \
  && docker-php-ext-install mysqli mbstring pdo pdo_mysql tokenizer xml soap sockets \
  && pecl clear-cache \
  && rm /var/cache/apk/*
