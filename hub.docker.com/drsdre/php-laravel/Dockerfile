FROM php:7.3-fpm-alpine

MAINTAINER Andre Schuurman <docker@drsdre.org>

LABEL Description="This image contains PHP 7.3 on alpine OS with extension needed for running Laravel applications" Vendor="Andre Schuurman" Version="7.3-fpm-alpine"

ARG EVENT_VER=event-2.4.3
ARG EV_VER=ev-1.0.4

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="10000" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="192" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

# Install production dependencies
RUN apk add --update --no-cache \
    bash \
    curl \
    #g++ \
    #gcc \
    git \
    imagemagick \
    icu-libs \
    libevent \
    libintl \
    libxslt \
    libzip \
    #make \
    mysql-client \
    nodejs \
    nodejs-npm \
    yarn \
    openssh-client \
    postgresql-libs \
    rsync

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    binutils \
    #curl-dev \
    freetype-dev \
    gettext-dev \
    icu-dev \
    imagemagick-dev \
    libc-dev \
    libevent-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libtool \
    libressl-dev \
    libxslt-dev \
    libxml2-dev \
    libzip-dev \
    postgresql-dev \
    sqlite-dev

# Install PECL and PEAR extensions
RUN pecl install imagick

# Install and enable php extensions
RUN docker-php-ext-enable imagick

# Configure PHP extensions
RUN docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Build and install PHP extensions
#RUN export CPU_COUNT=$(cat /proc/cpuinfo | grep processor | wc -l)
#RUN docker-php-ext-install -j$CPU_COUNT \
RUN docker-php-ext-install \
    bcmath \
    #ctype \ # Already available
    #curl \ # Already available
    exif \
    gd \
    gettext \
    #iconv \ # Already available
    intl \
    #json \ # Already available
    #mbstring \ # Already available
    opcache \
    pcntl \
    #pdo \ # Already available
    pdo_mysql \
    pdo_pgsql \
    #pdo_sqlite \ # Already available
    #simplexml \ # Already available
    sockets \
    #tokenizer \ # Already available
    #xml \ # Already available
    xsl \
    zip

# make sockets extension load first
RUN cd /usr/local/etc/php/conf.d/ && \
    mv docker-php-ext-sockets.ini 1-docker-php-ext-sockets.ini

COPY conf.d/opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Install PHP PECL extensions
RUN cd /usr/src && \
    pecl channel-update pecl.php.net

# Redis connector
RUN pecl install -o -f redis && docker-php-ext-enable redis

# Efficient data structures for PHP 7, provided as an alternative to the array. https://www.php.net/manual/en/intro.ds.php
#RUN pecl install -o -f ds && docker-php-ext-enable ds

# igbinary stores php data structures in a compact binary form: https://github.com/igbinary/igbinary
#RUN pecl install -o -f igbinary && docker-php-ext-enable igbinary

# Async programming Framework for PHP https://www.swoole.co.uk/
#RUN pecl install -o -f swoole && docker-php-ext-enable swoole

# High performance event loops https://www.php.net/manual/en/intro.ev.php
#RUN pecl download $EVENT_VER $EV_VER \
#    && tar -xf $EVENT_VER.tgz && cd $EVENT_VER && phpize \
#    && ./configure --with-event-core --with-event-pthreads --with-event-extra --with-event-openssl \
#    && make -j$CPU_COUNT && make install && cd .. \
#    && tar -xf $EV_VER.tgz && cd $EV_VER && phpize && ./configure && make -j$CPU_COUNT && make install && cd .. \
#    && docker-php-ext-enable event ev

# Change memory limit
RUN echo 'memory_limit = 2G ' >> /usr/local/etc/php/php.ini

# make the entrypoint executable
RUN chmod a+x /usr/local/bin/docker-php-entrypoint

# restrict console commands execution for web scripts
RUN chmod o-rx /bin/busybox /usr/bin/curl /usr/local/bin/pecl

# Cleanup
RUN apk del -f .build-deps && \
    rm -rf event* ev* /tmp/*  ~/.pearrc
