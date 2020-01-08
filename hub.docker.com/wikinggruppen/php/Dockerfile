# More docker config https://hub.docker.com/r/phpdocker/phpdocker/~/dockerfile/
FROM php:7.1-apache

# php gd support: libjpeg62-turbo-dev libpng12-dev gd
RUN apt-get update && apt-get install -my wget gnupg -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
		libxml2-dev \
        zlib1g \
        ssh \
        sshpass \
        libc-client-dev \
        libkrb5-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache \
	&& docker-php-ext-install soap \
    && docker-php-ext-install zip \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j$(nproc) imap

# PHP database extensions database (mysql)
RUN docker-php-ext-install -j$(nproc) mysqli pdo pdo_mysql

# Xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

# PHP EXIF
RUN docker-php-ext-install exif

# PHP
# intl
RUN apt-get update \
	&& apt-get install -y libicu-dev \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install intl

# HTACCESS rewrite
RUN a2enmod rewrite

# install Imagemagick & PHP Imagick ext
RUN apt-get update && apt-get install -y \
        libmagickwand-dev --no-install-recommends \
		&& pecl install imagick && docker-php-ext-enable imagick

# Install exim
RUN apt-get update && apt-get install -y exim4 && rm -r /var/lib/apt/lists/*

# Create public_html directory
RUN mkdir -p /var/www/public_html

# Add a symbolic link to the www directory & create the directory
RUN ln -s /var/www/public_html /var/www/www \
	&& mkdir -p /var/www/www

# Copy configuration
COPY config/php/opcache.ini $PHP_INI_DIR/conf.d/
COPY config/php/php.ini /usr/local/etc/php/php.ini
COPY config/xdebug/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY config/apache/apache.conf /etc/apache2/sites-enabled/000-default.conf
COPY config/apache/ports.conf /etc/apache2/ports.conf
COPY config/apache/ports.conf /etc/apache2/ports.conf
COPY config/exim4/exim4.conf /etc/exim4/exim4.conf
