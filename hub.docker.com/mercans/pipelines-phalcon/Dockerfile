FROM mercans/pipelines-php:1.0.0

MAINTAINER anton.pelesev@mercans.ee

RUN apk update && apk add \
    php5-pdo_mysql \
    php5-phalcon

RUN echo "extension=phalcon.so" > /etc/php5/conf.d/phalcon.ini

RUN rm -rf /var/cache/apk/*
