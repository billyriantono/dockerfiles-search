FROM php:7.2-fpm
RUN apt-get update && apt-get install -y \
        libicu-dev \
        apt-utils \
        curl \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install -j$(nproc) mbstring \
    && docker-php-ext-install -j$(nproc) opcache
RUN curl -sS https://getcomposer.org/installer | \
            php -- --install-dir=/usr/bin/ --filename=composer
EXPOSE 443
EXPOSE 80
EXPOSE 22
