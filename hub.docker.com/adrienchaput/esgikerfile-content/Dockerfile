FROM php:7.1-fpm

RUN apt-get update && apt-get install -y docker gnupg openssl libmcrypt-dev zlib1g-dev mysql-client git zip unzip git
RUN curl --silent --location https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN docker-php-ext-install -j$(nproc) pdo_mysql mcrypt mbstring zip
RUN docker-php-ext-enable zip
