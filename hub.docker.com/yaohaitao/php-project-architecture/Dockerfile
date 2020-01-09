FROM php:7.1-apache 

RUN pecl install xdebug 
RUN docker-php-ext-enable xdebug 
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/php.ini

RUN apt-get update \
        && apt-get install -y zlib1g-dev libicu-dev g++ \
        && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install intl \
        && docker-php-ext-install pdo pdo_mysql \
        && docker-php-ext-install mysqli
#RUN docker-php-ext-install zip
#RUN docker-php-ext-install mbstring
#RUN docker-php-ext-install mcrypt

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/ssl-cert-snakeoil.key -out /etc/ssl/certs/ssl-cert-snakeoil.pem -subj "/C=US/ST=Dev/L=Dev/O=Dev/OU=Dev/CN=localhost"

RUN a2enmod rewrite
RUN a2ensite default-ssl
RUN a2enmod ssl

EXPOSE 80
EXPOSE 443
