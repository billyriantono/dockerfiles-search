FROM wordpress:5.1.1-php7.1-apache

RUN docker-php-source extract && \
    pecl install redis && \
    docker-php-ext-install mysqli pdo pdo_mysql && \
    docker-php-ext-enable redis && \
    docker-php-source delete
