FROM php:7.2-fpm

MAINTAINER Tuan-Anh Nguyen <tuananhht94@gmail.com>

RUN apt-get update

RUN apt-get install -y git zip unzip

RUN apt-get install -y libmcrypt-dev mysql-client \
    && docker-php-ext-install pdo_mysql

# Install Xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

RUN apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libssl-dev \
    && pecl install mongodb \
    && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/ext-mongodb.ini \
    && echo "upload_max_filesize = 5M" > /usr/local/etc/php/conf.d/upload.ini \
    && docker-php-ext-install iconv mbstring exif zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
