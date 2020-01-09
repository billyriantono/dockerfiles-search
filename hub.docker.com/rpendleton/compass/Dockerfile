FROM rpendleton/nginx-php:latest
ENV DATE 2018-07-28

RUN curl -L https://github.com/aaronpk/Compass/archive/master.zip > /tmp/master.zip && \
    unzip -d /var /tmp/master.zip && \
    mv /var/Compass-master/compass /var/compass && \
    rm -rf /tmp/master.zip /var/Compass-master

WORKDIR /var/compass
RUN COMPOSER_ALLOW_SUPERUSER=1 composer install -o
RUN chown -R www-data: storage

COPY conf/env .env
COPY conf/supervisord.conf /etc/supervisor/conf.d/compass.conf
COPY conf/default.vhost /etc/nginx/conf.d/default.vhost
