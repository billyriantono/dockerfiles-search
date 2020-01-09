FROM alpine

MAINTAINER Aiden Andrews-McDermott <aj@peoplerange.com>

RUN set -x \
# create nginx user/group first, to be consistent throughout docker variants
    && addgroup -g 101 -S nginx \
    && adduser -S -D -H -u 101 -h /var/cache/nginx -s /sbin/nologin -G nginx -g nginx nginx

RUN apk --no-cache add php php-cli php-fpm php-tokenizer php-session php-json php-mbstring php-curl php-pdo php-pdo_mysql mariadb-client php-curl php-xml curl php-xml php-mysqlnd php-mysqli php-gd php-iconv php-zip php-dom php-fileinfo

RUN rm /etc/php7/php-fpm.d/www.conf
RUN rm /etc/php7/php.ini

ADD www.conf /etc/php7/php-fpm.d/www.conf
ADD php.ini /etc/php7/php.ini

RUN mkdir -p /run/php

EXPOSE 9000

CMD /usr/sbin/php-fpm7 --nodaemonize --fpm-config /etc/php7/php-fpm.d/www.conf
