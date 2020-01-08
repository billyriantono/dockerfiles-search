FROM arm32v7/php:fpm-alpine

COPY qemu-arm-static /usr/bin/qemu-arm-static

RUN /usr/bin/qemu-arm-static /bin/sh -c 'apk add --no-cache libzip-dev && \
    docker-php-ext-install mysqli zip pdo_mysql\
    && rm /usr/bin/qemu-arm-static'
