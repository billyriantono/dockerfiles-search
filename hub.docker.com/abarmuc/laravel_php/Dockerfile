FROM php:7.2-fpm
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y libmcrypt-dev
RUN apt-get install -y libmagickwand-dev --no-install-recommends
RUN apt-get install -y libpng-dev
RUN pecl install imagick
RUN docker-php-ext-enable imagick
RUN pecl install mcrypt-1.0.2
RUN docker-php-ext-enable mcrypt
RUN docker-php-ext-install pdo_mysql
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN apt-get install -y git
RUN apt-get update
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install zip \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd

COPY php_upload.ini /usr/local/etc/php/conf.d/uploads.ini

WORKDIR /var/www
