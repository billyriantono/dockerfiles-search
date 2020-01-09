FROM php:7.2.2-apache-stretch

MAINTAINER yakeworld@gmail.com 

RUN apt update \
    && apt -y --no-install-recommends install wget unzip \        
    && wget https://www.php-proxy.com/download/php-proxy.zip -O /tmp/php-proxy.zip \
    && unzip /tmp/php-proxy.zip -d /var/www/html/ \
    && rm /tmp/*.zip \
    && chown -R www-data:www-data /var/www/html 
