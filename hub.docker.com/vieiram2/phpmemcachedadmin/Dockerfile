FROM php:7.0-apache

RUN apt-get update && apt-get install -y libmemcached-dev zlib1g-dev \
  && pecl install memcached \
  && docker-php-ext-enable memcached \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

COPY config/php.ini /usr/local/etc/php/
COPY src/ /var/www/html/
COPY config/docker-php-entrypoint /usr/local/bin/
RUN chown -R www-data /var/www/html/Config /var/www/html/Temp
