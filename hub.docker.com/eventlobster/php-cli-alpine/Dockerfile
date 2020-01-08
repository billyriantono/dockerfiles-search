FROM php:7.3-cli-alpine
RUN apk add libxml2-dev libzip-dev zip unzip
RUN docker-php-ext-install pdo_mysql opcache bcmath soap zip
COPY --from=composer:1.9 /usr/bin/composer /usr/local/bin/composer
WORKDIR /var/www