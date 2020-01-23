FROM php:7.0.16-cli
MAINTAINER halito! <devs@halito.com>

# Update
RUN apt-get update

# Readd PHP extesions (GD) in order to active JPEG support
# Download extension dependencies
RUN apt-get install -y \
    libcurl3-dev \
    libxml2-dev \
    libzzip-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libicu-dev \
    libpng-dev \
    libjpeg-dev \
    libpng12-dev \
    libedit-dev \
    && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install pdo \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install curl \
    && docker-php-ext-install xml \
    && docker-php-ext-install zip \
    && docker-php-ext-install gd \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install intl \
    && docker-php-ext-install readline

# Configure extension
RUN docker-php-ext-configure gd \
    --with-gd \
    --with-jpeg \
    --with-gif \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    && docker-php-ext-install gd