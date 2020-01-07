# nginx proxy, confd and supervisord on Ubuntu Trusty
FROM markusma/nginx:1.7
MAINTAINER Markus Mattinen <markus@gamma.fi>

ADD config/etc/confd /etc/confd
ADD config/etc/nginx /etc/nginx
ADD config/etc/supervisor/conf.d /etc/supervisor/conf.d
ADD config/init /init

EXPOSE 80 443
