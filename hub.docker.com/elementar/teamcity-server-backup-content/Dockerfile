FROM php:7-fpm
# Install modules
RUN buildDeps="libpq-dev libzip-dev libfreetype6-dev libjpeg62-turbo-dev libpng12-dev " && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install pdo pdo_pgsql pgsql gd
CMD ["php-fpm"]
