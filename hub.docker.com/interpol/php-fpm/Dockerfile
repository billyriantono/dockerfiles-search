FROM php:7.2-fpm-alpine
WORKDIR /application

ENV PHALCON_VERSION=4.0.0
RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc libstdc++ binutils gmp isl libgomp \
    libatomic mpfr3 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install Phalcon ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    set -xe && \
    curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz && \
    cd cphalcon-${PHALCON_VERSION}/build && \
    sh install && \
    echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini && \
    cd ../.. && \
    rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION} && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libstdc++ libgcc mpc1 mpfr3 isl gmp && \
    rm -rf /var/cache/apk/*

RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc libstdc++ binutils gmp isl libgomp \
    libatomic mpfr3 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install PECL extention +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    pecl install psr && \
    echo "extension=psr.so" > /usr/local/etc/php/conf.d/psr.ini && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    apk add zlib-dev libmemcached-dev cyrus-sasl-dev && \
    pecl install memcached && \
    docker-php-ext-enable memcached && \
    apk add libmcrypt-dev && \
    pecl install mcrypt && \
    docker-php-ext-enable mcrypt && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb && \
    pecl install redis && \
    docker-php-ext-enable redis && \
    apk add unixodbc-dev && \
    pecl install sqlsrv && \
    docker-php-ext-enable sqlsrv && \
    pecl install pdo_sqlsrv && \
    docker-php-ext-enable pdo_sqlsrv && \
    apk add imagemagick-dev && \
    pecl install imagick && \
    docker-php-ext-enable imagick && \
    pecl clear-cache && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libstdc++ libgcc mpc1 mpfr3 isl gmp && \
    rm -rf /var/cache/apk/*

RUN echo "Install packages +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk update && \
    apk add musl m4 libbz2 perl autoconf pkgconf dpkg-dev dpkg libmagic file libgcc libstdc++ binutils gmp isl libgomp \
    libatomic mpfr3 mpc1 gcc musl-dev libc-dev g++ make re2c musl-utils && \
    echo "Install extention ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    docker-php-ext-install -j$(nproc) opcache && \
    apk add postgresql-dev && \
    docker-php-ext-install -j$(nproc) pdo_pgsql && \
    docker-php-ext-install -j$(nproc) pgsql && \
    docker-php-ext-install -j$(nproc) pdo_mysql && \
    docker-php-ext-install -j$(nproc) mysqli && \
    apk add libzip-dev && \
    docker-php-ext-install -j$(nproc) zip && \
    apk add imap-dev bzip2-dev && \
    docker-php-ext-install -j$(nproc) bz2 && \
    docker-php-ext-install -j$(nproc) bcmath && \
    apk add icu-dev && \
    docker-php-ext-install -j$(nproc) intl && \
    apk add gettext-dev && \
    docker-php-ext-install -j$(nproc) gettext && \
    apk add freetype-dev libjpeg-turbo-dev libpng-dev libwebp-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ --with-webp-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    apk add imap-dev openssl-dev krb5-dev && \
    PHP_OPENSSL=yes docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos && \
    docker-php-ext-install -j$(nproc) imap && \
    docker-php-ext-install -j$(nproc) calendar && \
    docker-php-ext-install -j$(nproc) exif && \
    apk add openldap-dev && \
    docker-php-ext-install -j$(nproc) ldap && \
    apk add libxml2-dev && \
    docker-php-ext-install -j$(nproc) soap && \
    docker-php-ext-install -j$(nproc) sockets && \
    docker-php-ext-install -j$(nproc) xmlrpc && \
    apk add tidyhtml-dev && \
    docker-php-ext-install -j$(nproc) tidy && \
    echo "Remove packages ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++" && \
    apk del autoconf m4 dpkg-dev perl dpkg file g++ gcc binutils libatomic libgomp libc-dev musl-dev make pkgconf \
    re2c libbz2 libmagic libstdc++ libgcc mpc1 mpfr3 isl gmp && \
    rm -rf /var/cache/apk/*
