FROM php:7.1-cli
RUN apt-get update && \
    apt-get install -y wget libssl-dev && \
    pecl install mongodb && \
    echo extension=mongodb.so > /usr/local/etc/php/conf.d/php.ini
    
