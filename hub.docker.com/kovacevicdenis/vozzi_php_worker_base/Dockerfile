FROM php:7.2-alpine

RUN apk --update add wget \
  curl \
  git \
  build-base \
  libmemcached-dev \
  libmcrypt-dev \
  libxml2-dev \
  zlib-dev \
  autoconf \
  cyrus-sasl-dev \
  libgsasl-dev \
  nano \
  vim \
  supervisor

RUN docker-php-ext-install mysqli mbstring pdo pdo_mysql tokenizer xml pcntl
RUN pecl channel-update pecl.php.net && pecl install memcached mcrypt-1.0.1 && docker-php-ext-enable memcached

###########################################################################
# bcmath:
###########################################################################

RUN docker-php-ext-install bcmath

RUN rm /var/cache/apk/* \
    && mkdir -p /var/www

###########################################################################
# Supervisord Configuration:
###########################################################################

COPY ./supervisord.d/ /etc/supervisord.d
COPY ./supervisord.conf /etc/supervisord.conf

###########################################################################
# Final touch:
###########################################################################

RUN mkdir -p /var/www/storage/logs

WORKDIR /var/www

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
