FROM php:7.3-fpm

RUN addgroup --gid 3000 --system rshop && adduser --uid 3000 --system --gid 3000 rshop

RUN apt-get update && apt-get install -y \
        gettext-base \
        libbz2-dev \
        libc-client-dev \
        libfreetype6-dev \
        libicu-dev \
        libjpeg62-turbo-dev \
        libkrb5-dev \
        libmagickwand-dev \
        libmcrypt-dev \
        libmemcached-dev \
        libxml2-dev \
        libzip-dev \
        zlib1g-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j "$(nproc)" \
        bcmath \
        bz2 \
        calendar \
        exif \
        gd \
        iconv \
        imap \
        intl \
        mysqli \
        opcache \
        pdo_mysql \
        soap \
        zip \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && pecl install channel://pecl.php.net/mcrypt-1.0.3 \
    && docker-php-ext-enable mcrypt \
    && pecl install memcached \
    && docker-php-ext-enable memcached \
    && pecl install redis \
    && docker-php-ext-enable redis

ENV PHP_DISPLAY_ERRORS Off
ENV PHP_MAX_EXECUTION_TIME 30
ENV PHP_MEMORY_LIMIT 128M
ENV PHP_OPCACHE_REVALIDATE_FREQ 0
ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS 0
ENV PHP_UPLOAD_MAX_FILESIZE 8M
ENV PHP_SESSION_SAVE_HANDLER files
ENV PHP_SESSION_SAVE_PATH /tmp
ENV PHP_SESSION_GC_MAXLIFETIME 1440

ENV FPM_LISTEN 127.0.0.1:9000
ENV FPM_MAX_CHILDREN 4
ENV FPM_START_SERVERS 2
ENV FPM_MIN_SPARE_SERVERS 1
ENV FPM_MAX_SPARE_SERVERS 3

COPY conf.d/* /usr/local/etc/php/conf.d/
COPY php-fpm.d/www.conf /usr/local/etc/php-fpm.d/www.conf

CMD envsubst < /usr/local/etc/php-fpm.d/www.conf > /usr/local/etc/php-fpm.d/www.conf && php-fpm
