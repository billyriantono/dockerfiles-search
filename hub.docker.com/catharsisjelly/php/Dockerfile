FROM php:7.3-fpm
COPY php.ini /usr/local/etc/php/php.ini
RUN apt-get update \
    && apt-get install -y libpng-dev unzip libicu-dev libzip-dev \
    && docker-php-ext-install pdo_mysql bcmath gd zip intl \
    && pecl install xdebug && echo "zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini \
    && apt autoremove -y && apt-get clean && apt-get purge
