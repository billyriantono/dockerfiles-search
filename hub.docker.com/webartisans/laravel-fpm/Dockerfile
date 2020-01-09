FROM php:7-fpm

ADD ./php.ini /usr/local/etc/php/

# Install required/useful PHP extensions
# OpenSSL, PDO and Tokenizer are included by default in the php:7-fpm Dockerfile.

RUN apt-get update && apt-get install -y \
    git \
    libbz2-dev \
    libcurl4-openssl-dev \
    libmcrypt-dev \
    libpq-dev \
    wget \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install -j$(nproc) bz2 curl mcrypt mbstring json zip

# Set up Composer
RUN wget https://getcomposer.org/composer.phar
RUN chmod +x composer.phar
RUN mv composer.phar /usr/local/bin/composer

# Set up PHPUnit
RUN wget https://phar.phpunit.de/phpunit.phar
RUN chmod +x phpunit.phar
RUN mv phpunit.phar /usr/local/bin/phpunit

# Set Up App Dir
RUN mkdir /app
WORKDIR /app