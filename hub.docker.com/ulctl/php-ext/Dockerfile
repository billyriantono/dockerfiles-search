FROM php:7.3

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
            build-essential \
            git \
            libfreetype6-dev \
            libicu-dev \
            libjpeg62-turbo-dev \
            libpng-dev \
            libxml2-dev \
            libzip-dev \
            zlib1g-dev \
            libmcrypt-dev \
            openssh-client \
            unzip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) \
            bcmath \
            gd \
            intl \
            soap \
            zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
