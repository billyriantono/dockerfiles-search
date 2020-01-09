FROM php:7.2-apache

RUN mkdir /app
COPY entry-point.sh /app/entry-point.sh
WORKDIR /var/www

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY apache2.conf /etc/apache2/apache2.conf
COPY php.ini /usr/local/etc/php/

RUN set -xe; \
    a2enmod rewrite; \
    apt-get update; \
    apt-get install -y libcurl4-gnutls-dev openssl libssl-dev libpng-dev libreadline-dev libpq-dev; \
    docker-php-ext-install bcmath calendar curl dba exif ftp gd hash mbstring mysqli opcache pcntl pdo pdo_mysql sockets zip; \
    \
    curl -sS https://getcomposer.org/installer | php; \
    mv composer.phar /usr/local/bin/composer; \
    apt-get clean

CMD ["bash", "/app/entry-point.sh"]
EXPOSE 80/tcp
