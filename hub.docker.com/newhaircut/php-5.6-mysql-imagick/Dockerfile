FROM php:5.6-apache

RUN mkdir -p /var/www

EXPOSE 80
EXPOSE 443

# Make sure rewrite mod is on
RUN a2enmod rewrite

# Install PHP has extensions
RUN apt-get update && \
    apt-get install -y \
        vim \
        php5-dev \
        php5-intl \
        cron \
        php5-curl \
        libmagickwand-dev --no-install-recommends && \
    rm -rf /var/lib/apt/lists/* && \
    pecl install imagick

RUN docker-php-ext-install pdo && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-enable imagick

# Update rights
RUN chown -R www-data:www-data /var/www
