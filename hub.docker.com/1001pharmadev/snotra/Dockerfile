FROM php:5.6

RUN apt-get update && apt-get install -y \
    curl \
    supervisor \
    git \
    zip

RUN mkdir -p /var/log/supervisor
COPY docker/worker/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN docker-php-ext-install pdo_mysql bcmath
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY docker/worker/php.ini /usr/local/etc/php

COPY . /var/www/html/
WORKDIR /var/www/html

RUN composer install

CMD ["/usr/bin/supervisord"]
