FROM php:7.1-cli

MAINTAINER Daniel Marynicz <daniel.maynicz@tvt.biz>

RUN apt-get update && apt-get install -y \
    openssl \
    git \
    unzip \
    libwebp-dev \
    libjpeg-dev \
    libbz2-dev \
    libcurl4-openssl-dev \
    libpng-dev \
    libmcrypt-dev \
    libpq-dev \
    libsqlite3-dev \
    libedit-dev \
    libzmq3-dev \
    procps



# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version



RUN docker-php-ext-install -j$(nproc) \
    bcmath \
    bz2 \
    calendar \
    curl \
    gd \
    json \
    mbstring \
    mcrypt \
    opcache \
    readline \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    pdo_sqlite \
    zip \
    pcntl \
    mysqli

RUN echo "short_open_tag = Off" >> /usr/local/etc/php/conf.d/short-open-tag.ini
RUN echo "memory_limit = 1G" >> /usr/local/etc/php/conf.d/memory-limit.ini

RUN pecl install zmq-beta
RUN docker-php-ext-enable zmq

#Install libicu
#mirrors:
#http://download.icu-project.org/files/icu4c/58.2/icu4c-58_2-src.tgz
#https://ftp.osuosl.org/pub/blfs/conglomeration/icu/icu4c-58_2-src.tgz
RUN mkdir /tmp/icu && \
    curl -sS -o /tmp/icu/icu.tar.gz -L  https://ftp.osuosl.org/pub/blfs/conglomeration/icu/icu4c-58_2-src.tgz && \
    tar -zxf /tmp/icu/icu.tar.gz -C /tmp/icu && \
    cd /tmp/icu/icu/source && \
    ./configure --prefix=/usr/local && \
    make -j$(nproc) && \
    make install && \
    rm -rf /tmp/icu

RUN docker-php-ext-configure intl --with-icu-dir=/usr/local
RUN docker-php-ext-install intl
