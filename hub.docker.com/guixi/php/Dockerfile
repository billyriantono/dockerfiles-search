FROM arm32v7/php:fpm-alpine

COPY qemu-arm-static /usr/bin/qemu-arm-static

RUN /usr/bin/qemu-arm-static /bin/sh -c 'apk add --no-cache libzip-dev libpng-dev freetype-dev libjpeg-turbo-dev ffmpeg zip'
RUN /usr/bin/qemu-arm-static /bin/sh -c 'docker-php-ext-configure gd --with-freetype --with-jpeg &&\
    docker-php-ext-install -j$(nproc) mysqli zip pdo_mysql exif gd\
    && rm /usr/bin/qemu-arm-static'
