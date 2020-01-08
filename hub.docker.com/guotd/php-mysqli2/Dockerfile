FROM php:7.0-fpm

# install mysql extension
RUN docker-php-ext-configure mysqli --with-mysqli=mysqlnd \
    && docker-php-ext-install mysqli pdo_mysql
