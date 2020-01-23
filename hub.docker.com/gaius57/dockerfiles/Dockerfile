FROM php:7.2-fpm-alpine

RUN apk update && apk add --no-cache \
    #required for xdebug
    $PHPIZE_DEPS \
    git \
    mysql-client \
    zlib-dev

RUN docker-php-ext-install \
    zip \
    pdo \
    pdo_mysql

RUN pecl install xdebug && docker-php-ext-enable xdebug
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Install Composer
RUN echo "Install composer globally" \
   && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
#   && composer install
