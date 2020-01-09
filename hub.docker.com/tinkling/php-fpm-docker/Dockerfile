FROM php:7.2-fpm

MAINTAINER Minh Khai <minhkhai97@gmail.com>

#install composer
RUN curl -s http://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# install npm

RUN apt-get update
RUN apt-get install -y gnupg gnupg1 gnupg2
RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install -y npm

# install dependencies
RUN apt-get update && apt-get install -y \
    libpq-dev \
    libmemcached-dev \
    curl \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    vim \
    unzip \
    git \
    curl \
    zlib1g-dev libicu-dev g++ \
    --no-install-recommends \
    && rm -r /var/lib/apt/lists/*

# configure mcrypt
RUN apt-get update \
    && apt-get install -y libmcrypt-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt

# install gmp allow for arbitrary-length integers to be worked
RUN apt-get update \
	&& apt-get install -y libgmp-dev re2c libmhash-dev libmcrypt-dev file \
	&& ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ \
	&& docker-php-ext-configure gmp \
    && docker-php-ext-install gmp

# configure gd library dynamically manipulating images under Ubuntu Linux LTS
RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-jpeg-dir=/usr/lib \
    --with-freetype-dir=/usr/include/freetype2

# Install extensions using the helper script provided by the base image
RUN docker-php-ext-install \
    bcmath \
    pdo_mysql \
    pdo_pgsql \
    gd \
    intl \
    zip

# add users
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# working directory
WORKDIR /var/www/laravel

ADD ./laravel.ini /usr/local/etc/php/conf.d
ADD ./laravel.pool.conf /usr/local/etc/php-fpm.d/

CMD ["php-fpm"]

# Expose port 9000 and start php-fpm server
EXPOSE 9000
