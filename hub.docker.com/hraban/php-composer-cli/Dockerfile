FROM php:7.1.10-cli

RUN apt-get update \
    && apt-get install -y \
    libxml2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    pkg-config \
    git

RUN pecl install mongodb -y \
    && touch  /usr/local/etc/php/conf.d30-mongodb.ini \
    && echo "extension=mongodb.so" | tee /usr/local/etc/php/conf.d/30-mongodb.ini

RUN docker-php-ext-install\
    zip \
    soap \
    pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir /root/.ssh
