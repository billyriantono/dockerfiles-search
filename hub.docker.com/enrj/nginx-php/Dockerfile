FROM richarvey/nginx-php-fpm:1.7.2

RUN apk update

RUN apk add autoconf automake make gcc g++ libtool pkgconfig libmcrypt-dev re2c nodejs npm pixman-dev cairo-dev pango-dev

RUN pecl install mongodb \
    && docker-php-ext-enable mongodb

COPY . .

# Image config
ENV SKIP_COMPOSER 1
ENV WEBROOT /var/www/html/public
ENV PHP_ERRORS_STDERR 1
ENV PHP_MEM_LIMIT 512
ENV REAL_IP_HEADER 1

# Laravel config
ENV APP_ENV dev
ENV APP_DEBUG true
ENV LOG_CHANNEL stderr

# Allow composer to run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

CMD ["/start.sh"]