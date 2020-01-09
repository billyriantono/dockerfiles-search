FROM php:7.1-fpm

LABEL vendor="UBIQUOS"
LABEL maintainer="Docker Team <docker@ubiquos.io>"

# Install PHP extensions
RUN apt-get update && \
    apt-get upgrade -qy && \
    apt-get install --no-install-recommends -y \
      cron \
      git \
      wget \
      libc-client-dev \
      libicu-dev \
      libkrb5-dev \
      libmcrypt-dev \
      libssl-dev \
      libz-dev \
      unzip \
      zip \
      nginx \
      nano \
      sudo \
      libgeoip-dev \
      libmemcached-dev \
      zlib1g-dev \
      systemd\
      libjpeg-dev \
  		libpng-dev \
      libtidy-dev \
      libbz2-dev \
      curl \
      libcurl4-openssl-dev \
      libedit-dev \
      libxml2-dev \
      wget

# Install New Relic
RUN curl -L https://download.newrelic.com/php_agent/release/newrelic-php5-8.5.0.235-linux.tar.gz | tar -C /tmp -zx && \
    export NR_INSTALL_USE_CP_NOT_LN=1 && \
    export NR_INSTALL_SILENT=1 && \
    /tmp/newrelic-php5-*/newrelic-install install && \
    rm -rf /tmp/newrelic-php5-* /tmp/nrinstall*



RUN apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false && \
    rm -rf /var/lib/apt/lists/* && \
    rm /etc/cron.daily/*

RUN docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos && \
    docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr && \
    docker-php-ext-install imap intl mbstring mysqli pdo_mysql zip gd opcache tidy bcmath bz2 curl exif json phar simplexml soap xml xmlrpc && \
    docker-php-ext-enable imap intl mbstring mysqli pdo_mysql zip gd opcache tidy bcmath bz2 curl exif json phar simplexml soap xml xmlrpc

RUN pecl install memcached && \
    docker-php-ext-enable memcached

RUN pecl install redis && \
    pecl install xdebug && \
    pecl install igbinary && \
    pecl install APCu &&\
    # pecl install geoip && \
    docker-php-ext-enable redis xdebug apcu igbinary

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# Define Nginx volume to persist data
VOLUME /var/www/html

EXPOSE 80

COPY default-nginx.conf /etc/nginx/sites-enabled/default

COPY test.php /var/www/html/test.php

COPY default-php.ini /usr/local/etc/php/conf.d/php.ini

COPY newrelic-php.ini /usr/local/etc/php/conf.d/newrelic.ini

COPY default-php-fpm.conf /usr/local/etc/php-fpm.d/www.conf
