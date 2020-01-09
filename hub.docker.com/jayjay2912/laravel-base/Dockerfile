FROM php:7.3-apache

# Install required packages
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y libzip-dev libxml2-dev && \
    apt-get autoremove -y && \
    pecl install -o -f redis && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

# Setup Apache modules and clear the sites
RUN a2enmod \
        rewrite \
        headers && \
    a2dismod \
        status && \
    rm -rf /tmp/* /etc/apache2/sites-enabled/*

# Install PHP extensions
RUN docker-php-ext-install \
        json \
        xml \
        pdo_mysql \
        mbstring \
        ctype \
        bcmath \
        zip && \
    docker-php-ext-enable \
        redis

# Setup Apache and the startup environment
COPY ./php.ini /usr/local/etc/php/php.ini
COPY ./apache2.conf /etc/apache2/apache2.conf
