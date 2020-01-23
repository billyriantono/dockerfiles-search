FROM php:7.1-fpm

MAINTAINER a691228@gmail.com

RUN apt-get update && apt-get install -y \
        libmcrypt-dev \
        libpq-dev \
        libsqlite3-dev \
        libcurl4-openssl-dev \
        libfreetype6-dev libjpeg62-turbo-dev libpng12-dev \
        libicu-dev \       
    && docker-php-ext-install -j$(nproc) iconv mcrypt  \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install -j$(nproc) pdo pdo_mysql pdo_pgsql pdo_sqlite mbstring curl json zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install opcache \
    && pecl install intl \
    && docker-php-ext-install -j$(nproc) intl

# Install bcmath
# RUN docker-php-ext-install bcmath


# Install GD
# RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev \
#     && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#     && docker-php-ext-install -j$(nproc) gd

# Install opcache
# RUN docker-php-ext-install opcache

# Install APCu
RUN pecl install apcu
RUN echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini

# Install intl
# RUN apt-get install -y libicu-dev \
#     && pecl install intl \
#     && docker-php-ext-install -j$(nproc) intl

# Install xdebug
RUN pecl install xdebug
RUN echo "zend_extenstion=/usr/local/lib/php/extensions/no-debug-non-zts-20151012/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini