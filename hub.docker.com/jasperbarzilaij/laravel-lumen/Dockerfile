FROM php:7.3-fpm-alpine

LABEL maintainer="Jasper Barzilaij <jasper@jbarzilaij.nl>"

RUN apk update \
    && apk add supervisor nginx composer nodejs npm \
    && docker-php-ext-install pdo_mysql

COPY ./supervisor/supervisord.conf /etc/supervisord.conf

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY ./php/php.ini /usr/local/etc/php/php.ini
COPY ./php-fpm/php-fpm.conf /usr/local/etc/php-fpm.conf
COPY ./php-fpm/www.conf /usr/local/etc/php-fpm.d/www.conf

RUN rm -rf /var/www/** \
    && adduser -DH www www \ 
    && chown www:www /var/www \
    && chown www:www /var/lib/nginx

COPY ./run /var/www/run

WORKDIR /var/www

EXPOSE 80

CMD ["/var/www/run"]
