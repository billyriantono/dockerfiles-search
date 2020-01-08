FROM php:7.0-alpine

ENV PHPIZE_DEPS \
    autoconf \
    file \
    g++ \
    gcc \
    libc-dev \
    make \
    pkgconf \
    re2c

RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    gnupg \
    libedit-dev \
    libxml2-dev \
    openssl-dev \
    sqlite-dev

RUN docker-php-ext-install \
    curl \
    exif \
    fileinfo \
    ftp \
    gd \
    hash \
    iconv \
    intl \
    json \
    ldap \
    mbstring \
    mcrypt \
    mysqli \
    opcache \
    pcntl \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    pdo_sqlite \
    pgsql \
    phar \
    posix \
    reflection \
    session \
    zip

RUN pecl install \
    xdebug \
&& docker-php-ext-enable \
    xdebug

RUN apk del .build-deps

EXPOSE 80
EXPOSE 8080

VOLUME ["/app"]
WORKDIR /app
