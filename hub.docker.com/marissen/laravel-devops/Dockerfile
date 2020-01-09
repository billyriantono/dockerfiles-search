FROM php:7.2

LABEL maintainer "Marissen timon@marissen.net"

RUN apt-get update && apt-get install -qy \
    git \
    curl \
    libmcrypt-dev \
    mariadb-client \
    zip \
    unzip \
    zlib1g-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    rsync \
    ssh \
    && apt-get clean

RUN docker-php-ext-configure gd

RUN docker-php-ext-install pdo_mysql bcmath zip gd exif

RUN php -r "readfile('https://getcomposer.org/installer');" | php && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

RUN curl -LO --silent https://deployer.org/deployer.phar && mv deployer.phar /usr/local/bin/dep && chmod +x /usr/local/bin/dep
