FROM php:7.2-fpm

LABEL maintainer "https://github.com/namtrung804"

ADD php.ini /usr/local/etc/php/

# composer
ENV COMPOSER_VERSION=1.7.2
RUN curl -L https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --version=${COMPOSER_VERSION} --install-dir=/usr/local/bin --filename=composer \
    && rm -f composer-setup.php

# php modules

RUN apt-get update -y \
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libxml2-dev zlib1g-dev unzip git jpegoptim optipng pngquant gifsicle --no-install-recommends --no-install-suggests \
    && apt-get clean -y \
    && pecl install redis xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-enable redis xdebug \
    && docker-php-ext-install mbstring xml opcache pdo_mysql mysqli soap zip session bcmath ctype dom hash sockets pdo fileinfo gettext xmlrpc xmlwriter

# cphalcon
RUN git clone https://github.com/phalcon/cphalcon \
    && cd cphalcon/build \
    && ./install \
    && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \
    && cd ../.. \
    && rm -rf cphalcon

# devtools
RUN git clone git://github.com/phalcon/phalcon-devtools.git \
    && cd phalcon-devtools/ \
    && ./phalcon.sh \
    && ln -s ~/phalcon-devtools/phalcon.php /usr/local/bin/phalcon

WORKDIR /app

RUN usermod -u 1000 www-data
