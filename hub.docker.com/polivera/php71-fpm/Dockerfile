FROM php:7.1.0-fpm
MAINTAINER Pablo Olivera

# Enable php extensions
RUN docker-php-ext-install -j$(nproc) mbstring json pdo pdo_mysql mysqli

# Adding install tools wget
RUN apt-get update && apt-get install -y -q --no-install-recommends wget unzip libmemcached-dev zlib1g-dev \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

# Install Memcached
WORKDIR /tmp/
RUN wget -O php-memcached.zip https://github.com/php-memcached-dev/php-memcached/archive/php7.zip \
    && unzip php-memcached.zip
WORKDIR /tmp/php-memcached-php7
RUN phpize \
    && ./configure \
    && make -j$(nproc) \
    && make install \
    && docker-php-ext-enable memcached

WORKDIR /var/www
RUN rm -Rf /tmp/*
