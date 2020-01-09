FROM php:7.1-fpm
MAINTAINER p.oliverav@gmail.com

RUN apt-get -qqy update \
    && apt-get install -y libpng-dev libjpeg-dev \
    && apt-get -y install re2c libmcrypt-dev \
    && apt-get -y install zlib1g-dev \
    && apt-get -y install libssl-dev libc-client2007e-dev libkrb5-dev \
    && apt-get -y install libcurl4-gnutls-dev \
    && apt-get -y install libxml2-dev libxslt-dev \
    && apt-get -y install libssl-dev \
    && apt-get -y install libcurl4-openssl-dev \
    && apt-get -y install git \
    && apt-get -y install libmemcached-dev \
    && apt-get -y install zip \
    && apt-get -y install libicu-dev \
    && apt-get -y install g++

RUN pecl install memcached-3.0.4 \
    docker-php-ext-enable memcached

RUN docker-php-ext-install bcmath \
    && docker-php-ext-configure gd --with-jpeg-dir=/usr/lib \
    && docker-php-ext-install gd \
    && docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-install imap \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install zip \
    && docker-php-ext-install soap \
    && docker-php-ext-install xmlrpc \
    && docker-php-ext-install intl \
    && docker-php-ext-install opcache


COPY moodle.php.ini /usr/local/etc/php/conf.d/php.ini
