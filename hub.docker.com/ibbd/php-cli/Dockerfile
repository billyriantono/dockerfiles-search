#
# PHP CLI Dockerfile
# - gd, iconv, mcrypt, pdo, mbstring, zip
# - redis
# - mongo
# - msgpack
# - memcache
# - mongo
# - swoole
# - composer
# - 
#
# https://github.com/ibbd/dockerfile-php-fpm
#
# 下载相关资源：./download.sh
# sudo docker build -t ibbd/php-cli ./
#

# Pull base image.
FROM php:5.6-cli

MAINTAINER Alex Cai "cyy0523xc@gmail.com"

# sources.list
# git clone git@github.com:IBBD/docker-compose.git
# 如果导致apt-get Install不成功，可以先注释这句
ADD ext/sources.list   /etc/apt/sources.list

# Install modules
RUN \
    apt-get update \
    && apt-get install -y \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libssl-dev \
    && rm -r /var/lib/apt/lists/*

# install php modules
# composer需要先安装zip
COPY ext/msgpack.tgz   /msgpack.tgz 
COPY ext/composer.php  /composer.php
RUN \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install iconv mcrypt pdo pdo_mysql tokenizer mbstring zip \
    && pecl install redis \
    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
    && pecl install memcache \
    && echo "extension=memcache.so" > /usr/local/etc/php/conf.d/memcache.ini \
    && pecl install /msgpack.tgz \
    && echo "extension=msgpack.so" > /usr/local/etc/php/conf.d/msgpack.ini \
    && pecl install mongo \
    && echo "extension=mongo.so" > /usr/local/etc/php/conf.d/mongo.ini \
    && pecl install swoole \
    && echo "extension=swoole.so" > /usr/local/etc/php/conf.d/swoole.ini \
    && cd / \
    && php composer.php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod 755 /usr/local/bin/composer \
    && composer config -g repositories.packagist composer http://packagist.phpcomposer.com \
    && rm -rf /msgpack.tgz \


WORKDIR /var/www 

# 解决时区问题
env TZ "Asia/Shanghai"

# Define mountable directories.
VOLUME /var/www


