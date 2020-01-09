FROM php:7.4-alpine

RUN apk add --update \
    git \
    unzip \
    npm \
    oniguruma-dev \
    curl-dev \
    icu-dev \
    libpng-dev \
    libxml2-dev \
    libzip-dev \
    bzip2-dev \
    mysql-client \
    openssh-client

# Install php extensions
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
    opcache \
    bcmath \
    tokenizer

# Install Composer
ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/bin/ --filename=composer

# Install Laravel Envoy
RUN composer global require "laravel/envoy"

# Install PHP_CodeSniffer and PHP CS Fixer
RUN composer global require "squizlabs/php_codesniffer"
RUN composer global require "friendsofphp/php-cs-fixer"

# Setup working directory
WORKDIR /var/www
