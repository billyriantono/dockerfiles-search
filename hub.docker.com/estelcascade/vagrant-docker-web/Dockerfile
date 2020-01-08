FROM php:7.1-apache

ENV APACHE_DOCUMENT_ROOT /var/www/html

RUN echo 'session.save_path=/var/www/tmp' > /usr/local/etc/php/conf.d/00_session.ini \
    ; mkdir /var/www/tmp \
    ; chown www-data:www-data /var/www/tmp
RUN a2enmod rewrite; a2enmod headers
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
    && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure pdo_mysql \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-configure mysqli \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-configure exif \
    && docker-php-ext-install -j$(nproc) exif\
    && docker-php-ext-configure opcache \
    && docker-php-ext-install -j$(nproc) opcache
