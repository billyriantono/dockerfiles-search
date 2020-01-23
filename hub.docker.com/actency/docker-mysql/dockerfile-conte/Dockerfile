FROM php:7.0.8-fpm-alpine

RUN apk update && apk add --no-cache git openssh-client openssl-dev libmcrypt-dev && \
    docker-php-ext-install mcrypt && \
    pecl install mongodb

RUN wget -O /tmp/composer.php https://getcomposer.org/installer && \
    php /tmp/composer.php --install-dir=/usr/local/bin --filename=composer && \
    rm -v /tmp/composer.php 
    
RUN composer global require "phpunit/phpunit=5.3.*" && \
    ln -sf /root/.composer/vendor/bin/phpunit /usr/local/bin/phpunit && \
    rm -rfv /root/.composer/cache

ADD mongodb.ini /usr/local/etc/php/conf.d/mongodb.ini

CMD "/usr/local/sbin/php-fpm"
