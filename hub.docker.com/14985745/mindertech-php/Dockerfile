FROM php:7.3-apache

RUN apt-get update \  
    && apt-get install -y \
        libmcrypt-dev \
        libz-dev \
	libzip-dev \
	libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        git \
        wget \
	supervisor \
    && pecl install mcrypt-1.0.3 \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install \
        mbstring \
        pdo_mysql \
	zip \
	bcmath \
    && docker-php-ext-enable mcrypt \
    && pecl install redis-5.1.1 \
    && docker-php-ext-enable redis

RUN apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl -sS https://getcomposer.org/installer \
        | php -- --install-dir=/usr/local/bin --filename=composer

RUN a2enmod rewrite
