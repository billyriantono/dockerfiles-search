FROM php:7.2-apache

WORKDIR /var/www/html

COPY app/ /var/www/html/

RUN  apt-get update && apt-get install -y default-mysql-server wget gnupg && \
        wget https://getcomposer.org/installer && php installer && \
        mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

EXPOSE 8000

CMD [ "php", "bin/console", "server:run", "0.0.0.0:8000" ]