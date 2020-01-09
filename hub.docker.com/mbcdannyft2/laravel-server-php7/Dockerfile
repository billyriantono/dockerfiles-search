FROM alpine

ENV php_conf /etc/php7/php.ini
ENV fpm_conf /etc/php7/php-fpm.conf

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && apk update

RUN apk add --no-cache busybox-static apk-tools-static && \
    apk.static upgrade --no-self-upgrade --available --simulate

RUN apk add --no-cache \
    tzdata \
    nginx \
    supervisor \
    curl

RUN cp /usr/share/zoneinfo/Europe/Copenhagen /etc/localtime

RUN apk add --no-cache \
    php7-opcache \
    php7-fpm \
    php7-mbstring \
    php7-pdo \
    php7-pdo_mysql \
    php7-openssl \
    php7-ctype \
    php7-phar \
    php7-curl \
    php7-intl \
    php7-mcrypt \
    php7-json \
    php7-mongodb

RUN mkdir -p /etc/nginx && \
    mkdir -p /var/www/app && \
    mkdir -p /run/nginx && \
    mkdir -p /var/log/supervisor

RUN ln -s /usr/bin/php7 /usr/bin/php

ADD conf/supervisord.conf /etc/supervisord.conf

RUN rm -Rf /etc/nginx/nginx.conf
ADD conf/nginx.conf /etc/nginx/nginx.conf

ADD conf/php-conf.ini /etc/php7/conf.d/00_conf.ini
ADD conf/php-fpm.conf /etc/php7/php-fpm.conf

RUN ln -s /etc/php7/php.ini /etc/php7/conf.d/php.ini && \
    find /etc/php7/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

RUN addgroup laravel \
 && adduser -s /bin/sh -D -H -G laravel laravel

RUN mkdir -p /srv/public
RUN mkdir -p /srv/storage/app/public
RUN mkdir -p /srv/storage/framework/cache
RUN mkdir -p /srv/storage/framework/sessions
RUN mkdir -p /srv/storage/framework/views
RUN mkdir -p /srv/storage/logs

RUN chown nginx:nginx /srv/storage/
RUN chown nginx:nginx /srv/storage/app
RUN chown nginx:nginx /srv/storage/app/public
RUN chown nginx:nginx /srv/storage/framework
RUN chown nginx:nginx /srv/storage/framework/cache
RUN chown nginx:nginx /srv/storage/framework/sessions
RUN chown nginx:nginx /srv/storage/framework/views
RUN chown nginx:nginx /srv/storage/logs

ADD init.py /init.py
RUN chmod 755 /init.py
ADD cron.py /cron.py
RUN chmod 755 /cron.py

RUN echo "#!/bin/sh\n/usr/bin/env php7 /srv/server/artisan" > /usr/bin/artisan
RUN chmod +x /usr/bin/artisan

EXPOSE 80
VOLUME /srv/server

CMD ["/init.py"]
