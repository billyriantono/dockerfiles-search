FROM php:7.3-fpm

RUN apt-get -y update \
    && apt-get -y install nginx supervisor \
    && rm -rf /var/lib/apt/lists/*

COPY nginx-config /etc/nginx/

COPY supervisord-config /etc/supervisor/conf.d/

WORKDIR /var/www/

VOLUME /var/www/

EXPOSE 80 443

CMD ["supervisord","-n","-c","/etc/supervisor/supervisord.conf"]
