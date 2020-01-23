FROM php:7.1-apache
RUN apt-get update && apt-get install libssl-dev curl git zlib1g-dev unzip libpng12-dev libjpeg-dev libpq-dev libicu-dev libmemcached-dev -y
RUN pecl install mongodb \
    && pecl install redis \
    && pecl install apcu \
    && pecl install memcached \
    && docker-php-ext-enable mongodb redis apcu memcached

RUN docker-php-ext-install gd mbstring opcache pdo pdo_mysql zip bcmath intl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY config/php.ini /usr/local/etc/php/

#
# Global Apache configuration changes
#
RUN sed -i \
    -e 's~^ServerSignature On$~ServerSignature Off~g' \
    -e 's~^ServerTokens OS$~ServerTokens Prod~g' \
    /etc/apache2/conf-enabled/security.conf