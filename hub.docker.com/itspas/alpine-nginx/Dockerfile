FROM itspas/alpine:3.3

MAINTAINER Yenole "Netxy@vip.qq.com"

RUN apk --update add \
  nginx \
  supervisor \
  && rm -rf /var/cache/apk/*

ADD nginx.conf /etc/nginx/nginx.conf

VOLUME ["/usr/share/nginx/html", "/etc/nginx/sites-enabled"]

ADD nginx.ini /etc/supervisor.d/nginx.ini

EXPOSE 80

CMD ["/usr/bin/supervisord"]
