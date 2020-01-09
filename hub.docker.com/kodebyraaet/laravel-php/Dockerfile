FROM php:7.3-fpm

RUN apt-get update \
    && apt-get install -y default-mysql-client zlib1g-dev libxml2-dev libmemcached-dev libpng-dev libsodium-dev cron libzip-dev curl --no-install-recommends \
    && pecl install memcached \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install soap \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install sodium \
    && docker-php-ext-install opcache \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install bcmath \
    && docker-php-ext-enable memcached \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

CMD php-fpm
