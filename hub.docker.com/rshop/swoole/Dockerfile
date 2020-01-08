FROM rshop/php:7.3-cli

RUN pecl install swoole \
    && docker-php-ext-enable swoole

EXPOSE 9501
