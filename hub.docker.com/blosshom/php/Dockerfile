FROM blosshom/php:7.1
MAINTAINER Aurélien Lavorel <contact@blosshom.com>

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo 'xdebug.remote_enable = On' >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
     echo 'xdebug.remote_autostart= On' >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
     echo 'xdebug.remote_connect_back = On' >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
