FROM php:7.2.8-apache-stretch
RUN apt-get update \
    && apt-get install -y postgresql-server-dev-9.6 libcurl4-gnutls-dev libpq-dev libmcrypt-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && a2enmod rewrite \
    && docker-php-ext-install curl pdo_pgsql pdo_mysql bcmath zip gd sockets \
    && pecl install -o -f apcu \
    && rm -rf /tmp/pear \
    && echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
COPY ./php.ini /usr/local/etc/php/
