FROM ubuntu:18.04

ENV PHP_VERSION 7.3
ENV PHP_IDE_CONFIG serverName=localhost
ENV COMPOSER_ALLOW_SUPERUSER 1

# Install required services.
RUN DEBIAN_FRONTEND=noninteractive apt-get update --yes --quiet && \
    DEBIAN_FRONTEND=noninteractive apt-get install --yes software-properties-common wget && \
    DEBIAN_FRONTEND=noninteractive add-apt-repository --yes ppa:ondrej/php && \
    DEBIAN_FRONTEND=noninteractive apt-get update --yes --quiet && \
    DEBIAN_FRONTEND=noninteractive apt-get install --yes \
        supervisor acl nginx ssl-cert git unzip \
		php${PHP_VERSION}-cli \
		php${PHP_VERSION}-curl \
		php${PHP_VERSION}-fpm \
		php${PHP_VERSION}-gmp \
		php${PHP_VERSION}-intl \
		php${PHP_VERSION}-json \
		php${PHP_VERSION}-mbstring \
		php${PHP_VERSION}-pgsql \
		php${PHP_VERSION}-readline \
		php${PHP_VERSION}-sqlite3 \
		php${PHP_VERSION}-xml \
		php${PHP_VERSION}-zip \
		php-redis \
		php-sodium \
		php-uuid \
		php-xdebug && \
    apt-get clean --yes --quiet && \
    rm --recursive --force /var/lib/apt/lists/* && \
    mkdir /run/php

# Install composer
RUN php --run "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php --run "unlink('composer-setup.php');" && \
    /usr/local/bin/composer global require hirak/prestissimo && \
    /usr/local/bin/composer global clear-cache

# Configure PHP
RUN sed --in-place -r "s/^;?memory_limit *=.*/memory_limit = 128M/" /etc/php/${PHP_VERSION}/cli/php.ini && \
    sed --in-place -r "s/php${PHP_VERSION}-fpm.sock/php-fpm.sock/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;clear_env = no/clear_env = no/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;?pm *=.*$/pm = dynamic/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;?pm\.max_children *= *[0-9]+/pm.max_children = 2048/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;?pm\.start_servers *= *[0-9]+/;pm.start_servers = 10/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;?pm\.min_spare_servers *= *[0-9]+/pm.min_spare_servers = 2/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;?pm\.max_spare_servers *= *[0-9]+/pm.max_spare_servers = 17/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf && \
    sed --in-place -r "s/^;?pm\.max_requests *= *[0-9]+/pm.max_requests = 120000/" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf

COPY etc/nginx/conf.d/* /etc/nginx/conf.d/
COPY etc/nginx/sites-available/* /etc/nginx/sites-available/
COPY etc/php/conf.d/* /etc/php/${PHP_VERSION}/cli/conf.d/
COPY etc/php/conf.d/* /etc/php/${PHP_VERSION}/fpm/conf.d/
COPY etc/php/mods-available/* /etc/php/${PHP_VERSION}/mods-available/
COPY etc/supervisor/conf.d/* /etc/supervisor/conf.d/

WORKDIR /var/www/html
