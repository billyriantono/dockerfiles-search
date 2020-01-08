FROM wordpress:fpm

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update && \
    apt-get install -y \
    git

RUN touch /var/log/php-fpm-error.log
COPY uploads.ini /usr/local/etc/php/conf.d/uploads.ini
