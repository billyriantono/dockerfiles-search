FROM alpine:latest

RUN apk update \
  && apk add bash nano nginx php7 \
  php7-redis php7-fpm php7-pdo_pgsql \
  php7-imap php7-pgsql php7-simplexml \
  php7-json php7-opcache php7-gd \
  php7-curl php7-iconv \
  supervisor

RUN mkdir -p /run/nginx /data /etc/supervisor/conf.d/

RUN rm -r /var/www/*
RUN rm -r /etc/nginx/conf.d/*

ADD config/supervisord.conf /etc/supervisord.conf
ADD config/website.conf /etc/nginx/conf.d/website.conf
ADD src/* /data/

VOLUME ["/etc/nginx","/var/www", "/data"]

EXPOSE 80

CMD ["/usr/bin/supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]

#CMD ["nginx", "-g", "daemon off;"]
