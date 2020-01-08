FROM php:5.5.32-fpm

RUN apt-get update && apt-get install -y php5-mysql mysql-client zlib1g-dev libmcrypt-dev cron awscli
RUN docker-php-ext-install -j$(nproc) zip mysqli mcrypt mbstring bcmath

COPY php-fpm.conf /usr/local/etc/
COPY php.ini /usr/local/etc/php/php.ini

EXPOSE 9000
CMD ["php-fpm", "-F", "-R"]
