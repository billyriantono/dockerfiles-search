FROM php:fpm

COPY ./config/custom.ini /usr/local/etc/php/conf.d/custom.ini

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
# Installing tools and PHP extentions using "apt", "docker-php", "pecl",
#

# Install "curl", "libmemcached-dev", "libpq-dev", "libjpeg-dev",
#         "libpng12-dev", "libfreetype6-dev", "libssl-dev", "libmcrypt-dev",
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libmemcached-dev \
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libssl-dev \
        libmcrypt-dev


# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql

#
# Install Laravel Dependencies
# - pcntl (Laravel Queues)
# - sockets (https://github.com/bschmitt/laravel-amqp)
#
RUN docker-php-ext-install pcntl \
    && docker-php-ext-install sockets

#####################################
# gd:
#####################################

# Install the PHP gd library
RUN docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
    docker-php-ext-install gd
