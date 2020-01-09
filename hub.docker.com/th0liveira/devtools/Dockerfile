FROM th0liveira/redis:5.0.6
FROM th0liveira/php:7.2.24
FROM th0liveira/nginx:1.16.1
FROM th0liveira/zat:3.4.0
FROM th0liveira/node:10.17.0
FROM composer:1.9.0
FROM th0liveira/jenkins:2.190.2

# MERGE CONTAINER IMAGES -----------------------------------------------------------

# -- copy redis-cli
COPY --from=th0liveira/redis:5.0.6 /usr/local/bin/redis-cli /usr/local/bin/redis-cli

# -- copy php (and disable fpm and xdebug)
COPY --from=th0liveira/php:7.2.24 / /
RUN rm /etc/supervisord/php-fpm.conf /usr/local/etc/php/conf.d/20-xdebug.ini

# -- copy ZAT
COPY --from=th0liveira/zat:3.4.0 / /

# -- copy Node
COPY --from=th0liveira/node:10.17.0 / /

# -- copy composer
COPY --from=composer:1.9.0 /usr/bin/composer /usr/bin/composer

# -- copy Nginx Certs
COPY --from=th0liveira/nginx:1.16.1 /etc/nginx/certs/* /etc/certs/

# -- copy jenkins
COPY --from=th0liveira/jenkins:2.190.2 / /

# PREPARE CONFIGURATIONS -----------------------------------------------------------

# -- configure composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /mnt/composer

# -- copy php.ini
COPY config/php.ini /etc/php.ini

# PREPARE DEPENDENCIES -------------------------------------------------------------

RUN apk add --no-cache --no-progress mysql-client

# CLEAR IMAGE ----------------------------------------------------------------------

RUN rm -rf /tmp/* /var/cache/apk/*

# DEFAULTS -------------------------------------------------------------------------

# EXPOSE PORT ----------------------------------------------------------------------

EXPOSE 4567

# PREPARE SUPERVISOR FILE ----------------------------------------------------------

# RUN COMMAND ----------------------------------------------------------------------
