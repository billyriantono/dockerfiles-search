ARG PHP_VERSION=7

FROM boulzy/php:$PHP_VERSION

RUN apk update && apk add php7-fpm

COPY /conf/app.conf /etc/php7/php-fpm.d/z00-listen.conf

EXPOSE 9000

CMD ["php-fpm7", "--nodaemonize"]
