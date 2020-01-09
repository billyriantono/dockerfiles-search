FROM alpine:3.4

WORKDIR /data

RUN apk --update add nginx php5-fpm && \
    mkdir -p /var/log/nginx && \
    touch /var/log/nginx/access.log && \
    mkdir -p /run/nginx 

RUN apk update \
    && apk add php5-openssl \
    && apk add php5-phar \
    && apk add php5-ctype \
    && apk add git \
    && apk add curl \
    && apk add php5-json \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && apk add inotify-tools \ 
    && apk add php5-dev \
    && apk add php5-mysql php5-mysqli \
    && apk add php5-zlib \
    && apk add supervisor 

ADD . /data
ADD ./docker/nginx/nginx.conf /etc/nginx/nginx.conf
ADD ./docker/php-fpm/php-fpm.conf /etc/php5/php-fpm.conf

RUN chmod -R a+w /data/web/app/uploads

RUN composer install

RUN mkdir -p /var/log/supervisor \
 && mkdir -p /etc/supervisor/conf.d

ADD ./docker/supervisor/supervisor.conf /etc/supervisor.conf
ADD ./docker/supervisor/services /etc/supervisor/conf.d

# Certbot
# RUN apk add --no-cache certbot
# VOLUME /etc/letsencrypt
# VOLUME /var/lib/letsencrypt
#COPY /etc/crontab /var/spool/cron/crontabs/certbot-renew

EXPOSE 80 443

ADD run.sh /run.sh
RUN ["chmod", "+x", "/run.sh"]

CMD /run.sh ${SERVER_ENV} ${MYSQL_USER} ${MYSQL_PASSWORD} ${MYSQL_HOST} ${WP_HOME}
