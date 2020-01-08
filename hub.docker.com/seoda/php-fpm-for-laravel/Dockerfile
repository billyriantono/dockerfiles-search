FROM php:7.2-fpm

RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libzip-dev git unzip libicu-dev libzstd-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install -j$(nproc) gd pdo_mysql zip pcntl bcmath intl \
    && yes | pecl install igbinary redis \
    && docker-php-ext-enable opcache igbinary redis \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer config -g repos.packagist composer https://packagist.jp && \
    composer global require hirak/prestissimo
