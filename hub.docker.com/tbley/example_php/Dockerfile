FROM alpine:3.10

RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk --no-cache add php7 php7-fpm php7-curl php7-pdo_mysql php7-json php7-pecl-apcu php7-mbstring \
        php7-phar php7-opcache php7-dom php7-tokenizer php7-simplexml php7-pecl-pcov@testing \
    && rm /etc/php7/conf.d/pcov.ini

RUN addgroup -g 82 -S www-data \
    && adduser -u 82 -h /var/www -D -S -G www-data www-data

# php global setting
COPY ./php.ini /etc/php7/php.ini

# php fpm settings
COPY ./php-fpm.conf /etc/php7/php-fpm.d/www.conf

WORKDIR /var/www

CMD [ "php-fpm7", "-F" ]
