FROM php:7.4-apache

# Update package repository
RUN apt-get update -y
# Intall tools
RUN apt-get install -y git zip
# Install libraries
RUN apt-get install -y \
    # curl
    libcurl4-gnutls-dev \
    # intl
    libicu-dev \
    # gd
    libjpeg-dev \
    libpng-dev \
    zlib1g-dev \
    libxpm-dev \
    libwebp-dev \
    libfreetype6-dev \
    # xml
    libxml2-dev \
    libexpat1-dev \
    # bz2
    libbz2-dev \
    # mbstring
    libonig-dev \
    # zip
    libzip-dev \
    # pspell_* functions
    libaspell-dev
# Install PHP extensions
RUN docker-php-ext-install \
    mbstring \
    pdo_mysql \
    curl \
    json \
    intl \
    gd \
    xml \
    zip \
    bz2 \
    opcache
# Install & enable Xdebug for code coverage reports
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
# Enable URL rewrite
RUN a2enmod rewrite && service apache2 restart
# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

WORKDIR /var/www/html/
