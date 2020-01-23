FROM php:7.3-apache

RUN apt-get update && apt-get install -y \
    unzip \
    libpng-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    pkg-config \
    libedit-dev \
    libxml2-dev \
    libzip-dev \
    imagemagick

RUN docker-php-ext-install intl gd curl opcache zip bcmath pdo_mysql soap sockets

RUN pecl channel-update pecl.php.net \
    && pecl install apcu-5.1.17 \
    && docker-php-ext-enable apcu

RUN { \
        echo 'opcache.memory_consumption=256'; \
        echo 'opcache.interned_strings_buffer=16'; \
        echo 'opcache.max_accelerated_files=32531'; \
        echo 'opcache.max_wasted_percentage=10'; \
        echo 'opcache.revalidate_freq=60'; \
        echo 'opcache.validate_timestamps=0'; \
        echo 'opcache.enable_cli=1'; \
        echo 'realpath_cache_size=4096K'; \
        echo 'realpath_cache_ttl=600'; \
    } > /usr/local/etc/php/conf.d/opcache-recommended.ini

RUN { \
        echo 'memory_limit=-1'; \
        echo 'upload_max_filesize=20M'; \
        echo 'post_max_size=20M'; \
    } > /usr/local/etc/php/conf.d/zz-overrides.ini

COPY --from=composer:1.8.4 /usr/bin/composer /usr/bin/composer
RUN composer global require hirak/prestissimo
