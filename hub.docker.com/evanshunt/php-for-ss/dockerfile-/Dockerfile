FROM php:7.0-fpm
RUN apt-get update
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install -j$(nproc) mcrypt
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo pdo_mysql