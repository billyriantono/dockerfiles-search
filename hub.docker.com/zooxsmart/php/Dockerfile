FROM php:7.4

MAINTAINER Leandro Silva <leandro.silva@zooxsmart.com>

# install modules 
RUN apt-get update && apt-get install -y \
        procps \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        openssl \
        libssh-dev \
        libpcre3 \
        libpcre3-dev \
        libnghttp2-dev \
        libhiredis-dev \
        libbz2-dev \
        libedit-dev \
        libxml2-dev \
	libsodium-dev \
	libzip-dev \
        libcurl4-openssl-dev \
        curl \
        wget \
        zip \
        unzip \
        vim \
	libonig-dev \
        libicu-dev \
        git && \
        apt autoremove && apt clean

# Install updated ICU
RUN cd /tmp && \
    curl -L -o /tmp/icu.tgz https://github.com/unicode-org/icu/releases/download/release-65-1/icu4c-65_1-src.tgz && \
    tar zxvf /tmp/icu.tgz && cd icu/source && \
    ./configure --prefix="/usr" --libdir=/usr/lib/x86_64-linux-gnu && make && make install

# install php ext
RUN docker-php-ext-configure gd --with-freetype --with-jpeg && \ 
    docker-php-ext-install \
    bcmath \
    bz2 \
    ctype \
    gd \
    gettext \
    intl \
    mbstring \
    mysqli \
    opcache \
    pcntl \
    pdo_mysql \
    soap \
    sockets \
    zip && \
    echo "opcache.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

#install redis
RUN pecl install redis mongodb && docker-php-ext-enable redis mongodb

# install composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update --clean-backups

# install swoole
#TIP: it always get last stable version of swoole coroutine.
RUN cd /root && \
    curl -L -o /tmp/swoole.tar.gz https://github.com/swoole/swoole-src/archive/v4.4.12.tar.gz && \
    tar zxvf /tmp/swoole.tar.gz && cd swoole-src* && \
    phpize && \
    ./configure \
    --enable-coroutine \
    --enable-openssl  \
    --enable-http2  \
    --enable-async-redis \
    --enable-mysqlnd && \
    make && make install && \
    docker-php-ext-enable swoole && \
    echo "swoole.fast_serialize=On" >> /usr/local/etc/php/conf.d/docker-php-ext-swoole-serialize.ini

# Cleanup
RUN rm -rf /tmp/*

# set China timezone
RUN echo 'UTC' > /etc/timezone && \
    echo "[Date]\ndate.timezone=UTC" > /usr/local/etc/php/conf.d/timezone.ini

