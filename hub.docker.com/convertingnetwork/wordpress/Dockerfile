FROM wordpress:4-php7.1-fpm-alpine
RUN apk add --no-cache libmcrypt-dev libltdl && \
    docker-php-ext-install mcrypt
    