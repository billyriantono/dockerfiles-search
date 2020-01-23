FROM php:7.2-fpm

RUN apt-get update \
        && apt-get install -y \
            zsh \
            vim \
            sudo \
            libssl-dev \
            libicu-dev \
            zlib1g-dev \
            libcurl4-openssl-dev \
            pkg-config \
            libsasl2-dev \
            libpcre3-dev \
            mysql-client \
            libmemcached-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN pecl channel-update pecl.php.net

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN docker-php-ext-install \
    intl \
    mysqli \
    opcache \
    pdo_mysql \
    zip

RUN pecl install memcached

RUN echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini

# Install PHP extension [Xdebug]
RUN pecl install -f xdebug-2.6.0 \
    && pecl clear-cache
#    && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20160303/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /var/www