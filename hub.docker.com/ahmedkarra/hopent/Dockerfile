FROM php:7.1.26-fpm-alpine3.8
LABEL Maintainer="小方老师<tech@ahaschool.com>" Description="ahaschool nginx php"

ENV site api

COPY docker-php-helper /usr/local/bin/
COPY src /tmp/src

# Install packages, autoconf g++ make 
# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk add nginx libmcrypt-dev librdkafka-dev && \
    docker-php-ext-install bcmath pdo_mysql mcrypt && \
    docker-php-helper init && docker-php-helper nginx && \
    rm -rf /var/cache/apk/ && mkdir -p /var/www/html /var/log/nginx

WORKDIR /var/www/html

VOLUME ['/var/www/html', '/var/log']

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["docker-php-helper", "start"]