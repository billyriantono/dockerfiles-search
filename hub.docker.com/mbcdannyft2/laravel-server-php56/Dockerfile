FROM alpine

ENV php_conf /etc/php5/php.ini
ENV fpm_conf /etc/php5/php-fpm.conf

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
    php5-opcache \
    php5-fpm \
    php5-pdo \
    php5-pdo_mysql \
    php5-openssl \
    php5-ctype \
    php5-phar \
    php5-curl \
    php5-intl \
    php5-mcrypt \
    php5-json

RUN mkdir -p /etc/nginx && \
    mkdir -p /var/www/app && \
    mkdir -p /run/nginx && \
    mkdir -p /var/log/supervisor

ADD conf/supervisord.conf /etc/supervisord.conf

RUN rm -Rf /etc/nginx/nginx.conf
ADD conf/nginx.conf /etc/nginx/nginx.conf

ADD conf/xx01-php-conf.ini /etc/php5/conf.d/
ADD conf/xx-php-fpm.conf /etc/php5/fpm.d/

#RUN mkdir -p /etc/nginx/sites-available/ && \
#    mkdir -p /etc/nginx/sites-enabled/ && \
#    mkdir -p /etc/nginx/ssl/
#
#ADD conf/nginx-site.conf /etc/nginx/sites-available/default.conf

#RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf

RUN ln -s /etc/php5/php.ini /etc/php5/conf.d/php.ini && \
    find /etc/php5/conf.d/ -name "*.ini" -exec sed -i -re 's/^(\s*)#(.*)/\1;\2/g' {} \;

RUN addgroup laravel \
 && adduser -s /bin/sh -D -H -G laravel laravel

RUN sed -i -e "s/user = nobody/user = nginx/g" ${fpm_conf} && \
    sed -i -e "s/group = nobody/group = nginx/g" ${fpm_conf} && \
    sed -i -e "s/;listen.mode = 0660/listen.mode = 0666/g" ${fpm_conf} && \
    sed -i -e "s/;listen.owner = nobody/listen.owner = nginx/g" ${fpm_conf} && \
    sed -i -e "s/;listen.group = nobody/listen.group = nginx/g" ${fpm_conf} && \
    sed -i -e "s/listen = 127.0.0.1:9000/listen = \/var\/run\/php-fpm.sock/g" ${fpm_conf}

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

ADD start.php /start.php
RUN chmod 755 /start.php
ADD cron.py /cron.py
RUN chmod 755 /cron.py

EXPOSE 80
VOLUME /srv/server

CMD ["/start.php"]
