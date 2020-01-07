FROM php:7.2-alpine

WORKDIR /root

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN composer require phpunit/phpunit =7.4.4 --prefer-dist

COPY . .

# ./vendor/bin/phpunit --bootstrap bootstrap.php test.php
# ./vendor/bin/phpunit --bootstrap bootstrap.php testInSeparatedProcess.php
