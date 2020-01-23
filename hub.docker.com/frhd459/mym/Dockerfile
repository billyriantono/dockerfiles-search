FROM php:7.1-apache
RUN a2enmod rewrite \
    && apt update \
    && apt-get install redis-server unzip curl libcurl4-gnutls-dev libicu-dev libmcrypt-dev libvpx-dev libjpeg-dev libpng-dev libxpm-dev zlib1g-dev libfreetype6-dev libxml2-dev libexpat1-dev libbz2-dev libgmp3-dev libldap2-dev unixodbc-dev libpq-dev libsqlite3-dev libaspell-dev libsnmp-dev libpcre3-dev libtidy-dev -yqq \
    && service redis-server start \
    && docker-php-ext-install mbstring curl json intl gd xml zip bz2 opcache pdo_pgsql \
    && pecl install redis-5.0.0 \
    && docker-php-ext-enable redis
