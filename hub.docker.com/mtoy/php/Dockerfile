FROM mtoy/php:7.2

ENV COMPOSER_CACHE_DIR /var/www/.composer

RUN apt-get update \
    && apt-get install -y gnupg2 \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y \
        git \
        zip \
        unzip \
        nodejs \
        --no-install-recommends \
    && npm install -g gulp yarn \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && rm -r /var/lib/apt/lists/*

ADD xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
