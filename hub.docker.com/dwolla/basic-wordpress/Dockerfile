
FROM alpine:3.8
MAINTAINER Dwolla Engineering <dev+marketing-wordpress@dwolla.com>

RUN apk --no-cache add php7 \
    php7-fpm \
    php7-mysqli \
    php7-pdo_mysql \
    php7-json \
    php7-openssl \
    php7-curl \
    php7-zlib \
    php7-xml \
    php7-phar \
    php7-intl \
    php7-dom \
    php7-xmlreader \
    php7-ctype \
    php7-mbstring \
    php7-gd \
    php7-simplexml \
    php7-tokenizer \
    php7-xmlwriter \
    php7-opcache \
    nginx \
    supervisor \
    curl

# configure NGINX, PHP-FPM, and Supervisor
COPY container-config/nginx.conf       /etc/nginx/nginx.conf
COPY container-config/fpm-pool.conf    /etc/php7/php-fpm.d/zzz_custom.conf
COPY container-config/php.ini          /etc/php7/conf.d/zzz_custom.ini
COPY container-config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# install Composer and PHP dependencies
WORKDIR /var/www/html/
COPY composer.json composer.json
COPY composer.lock composer.lock

ADD https://getcomposer.org/installer /tmp/composer-setup.php
RUN php /tmp/composer-setup.php --install-dir /usr/local/bin/ --filename composer \
 && rm /tmp/composer-setup.php \
 && php /usr/local/bin/composer install --no-scripts --no-dev \
 && rm -rf /usr/local/bin/composer

# copy remaining files to container
COPY config     config
COPY web        web
COPY wp-cli.yml wp-cli.yml

EXPOSE 80
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
