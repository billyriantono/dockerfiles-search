#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM php:7.3-fpm

LABEL maintainer="klgd <slice1213@gmail.com>"

RUN php -v

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
# Installing tools and PHP extentions using "apt", "docker-php", "pecl",
#

# Install "curl", "libmemcached-dev", "libpq-dev", "libjpeg-dev",
#         "libpng-dev", "libfreetype6-dev", "libssl-dev", "libmcrypt-dev",
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        libmemcached-dev \
        # libz-dev is zlib1g-dev
        libz-dev \
        libpq-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libssl-dev \
        libmcrypt-dev \
        libzip-dev

# Install the PHP gd library
RUN docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 \
    && docker-php-ext-install gd

# Install the php memcached extension
# https://github.com/php-memcached-dev/php-memcached
RUN pecl install memcached-3.1.3 && \
    docker-php-ext-enable memcached

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql \
    # Install the PHP pdo_pgsql extention
    && docker-php-ext-install pdo_pgsql \
    # Install the bcmath extension
    && docker-php-ext-install bcmath \
    # Install the Exif extension
    && docker-php-ext-install exif \
    # Install the Sockets extension
    && docker-php-ext-install sockets \
    # Install the zip extension
    && docker-php-ext-configure zip --with-libzip \
    # Install the zip extension
    && docker-php-ext-install zip \
    # Install the opcache extension
    && docker-php-ext-install opcache

# Copy opcache configration
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm -f /var/log/lastlog /var/log/faillog