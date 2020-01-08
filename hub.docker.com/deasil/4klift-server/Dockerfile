FROM php:7.3.5-fpm

# utils, build
RUN apt-get update \
    && apt-get install git libzip-dev autoconf libssl-dev zlib1g-dev libicu-dev g++ make cmake libuv1-dev libgmp-dev uuid-dev -y

RUN cd /usr/src/ \
    && git clone git://git.openssl.org/openssl.git \
    && cd openssl \
    && git checkout tags/OpenSSL_1_0_2k \
    && ./config shared -fPIC --prefix=/usr/local --openssldir=/usr/local/ssl \
    && make \
    && make depend \
    && make test \
    && make install \
    && ln -fs /usr/local/openssl/bin/openssl/bin/openssl /usr/bin

# datastax php-driver fox cassandra
RUN cd /usr/src/ \
    && git clone https://github.com/datastax/php-driver.git /usr/src/datastax-php-driver \
    && cd /usr/src/datastax-php-driver \
    && git checkout --detach v1.2.2 \
    && git submodule update --init \
    && cd ext \
    && ./install.sh \
    && echo "extension=cassandra.so" > /usr/local/etc/php/conf.d/cassandra.ini

## PHP extensions
RUN docker-php-ext-install zip mbstring intl opcache bcmath \
    && echo extension=bcmath.so > /usr/local/etc/php/conf.d/docker-php-ext-bcmath.ini \
    && pecl install apcu \
    && echo extension=apcu.so > /usr/local/etc/php/conf.d/apcu.ini \
    && pecl install uuid \
    && echo extension=uuid.so > /usr/local/etc/php/conf.d/uuid.ini

WORKDIR /app

EXPOSE 9000
