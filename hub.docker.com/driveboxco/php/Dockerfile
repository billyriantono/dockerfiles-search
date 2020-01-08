FROM php:7.3-fpm-stretch as backend

RUN apt-get update -yqq && apt-get install -y gnupg libmcrypt-dev libpq-dev locales libpng-dev libjpeg-dev libfreetype6-dev libzip-dev zlib1g-dev git libgmp-dev libxml2-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install gd \
    && docker-php-ext-install -j$(nproc) pgsql \
    && docker-php-ext-install pdo_pgsql \
    && docker-php-ext-install soap \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gmp \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb

RUN echo Europe/Warsaw >/etc/timezone && \
    ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

RUN locale-gen en_US.utf8 pl_PL.utf8 de_DE.utf8

RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer
