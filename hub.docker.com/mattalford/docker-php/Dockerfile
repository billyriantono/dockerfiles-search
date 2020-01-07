FROM php:7.2.10-fpm

MAINTAINER Matt Alford <malford@nsgdv.com>

ADD laravel.ini /usr/local/etc/php/conf.d
ADD laravel.pool.conf /usr/local/etc/php-fpm.d/

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        nano \
        libz-dev \
        libpq-dev \
        libssl-dev \
        libmcrypt-dev \
        libfreetype6-dev

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/local/bin \
        --filename=composer

RUN rm -r /var/lib/apt/lists/*

RUN usermod -u 1000 www-data

WORKDIR /var/www/app

CMD ["php-fpm"]

EXPOSE 9000
