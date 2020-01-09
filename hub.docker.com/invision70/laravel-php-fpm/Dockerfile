FROM php:7.1-fpm

WORKDIR /var/www/laravel
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV PATH="/root/.composer/vendor/bin:${PATH}"

RUN apt-get update && apt-get install -my \
    mcrypt \
    libmcrypt-dev \
    git \
    wget \
    unzip \
    gcc \
    make \
    autoconf \
    libc-dev \
    pkg-config \
    libmagickwand-dev \
    build-essential \
    imagemagick \
    mysql-client \
    postgresql-client \
    zlib1g-dev \
    libmemcached-dev \
    libssl-dev \
    libpq-dev

# Install PECL
ADD docker-php-pecl-install /usr/local/bin/
RUN chmod u+x /usr/local/bin/docker-php-pecl-install

RUN pecl install mongodb
# Install extensions
COPY setup.sh /setup.sh
RUN docker-php-ext-install mcrypt \
  && docker-php-ext-install gd \
  && docker-php-ext-install opcache \
  && docker-php-ext-install mysqli \
  && docker-php-ext-install pdo \
  && docker-php-ext-install pdo_mysql \
  && docker-php-ext-install pdo_pgsql \
  && docker-php-ext-install soap \
  && docker-php-ext-install sockets \
  && docker-php-ext-install bcmath \
  && docker-php-ext-install zip
RUN sh /setup.sh

# Add configuration files
COPY conf/php.ini /usr/local/etc/php/conf.d/40-custom.ini
COPY conf/www.conf /usr/local/etc/php-fpm.d/www.conf

COPY composer.phar /composer.phar
RUN /composer.phar global require "laravel/installer"

VOLUME ["/var/www/laravel"]
