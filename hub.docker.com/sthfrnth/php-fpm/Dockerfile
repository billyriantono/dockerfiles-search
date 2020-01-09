FROM php:5.6-fpm
ENV REFRESHED_AT 2016-01-17

RUN apt-get update && apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mbstring pdo_mysql tokenizer

COPY php-fpm/php.ini /usr/local/etc/php/

ADD . /var/www/html

CMD ["php-fpm"]
