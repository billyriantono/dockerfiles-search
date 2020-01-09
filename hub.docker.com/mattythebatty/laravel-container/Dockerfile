FROM php:7.1-fpm

MAINTAINER Matthew Tonkin-Dunn <mattythebatty@gmail.com>

ADD ./laravel.ini /usr/local/etc/php/conf.d
ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

RUN apt-get update && apt-get install -y \
    curl \
    git \
    zip \
    unzip \
    libjpeg-dev \
    libpng12-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    npm \
    --no-install-recommends \
    && rm -r /var/lib/apt/lists/*

RUN apt-get clean

# configure gd library
RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
    pdo_mysql \
    gd \
    mcrypt

RUN curl -s http://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN usermod -u 1000 www-data

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN npm install gulp -g

WORKDIR /var/www/laravel

CMD ["php-fpm"]

EXPOSE 9000

