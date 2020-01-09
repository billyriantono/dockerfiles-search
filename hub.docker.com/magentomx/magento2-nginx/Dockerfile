FROM nginx:1.10.1
MAINTAINER Eduardo Garcia <eduardo.gb.isc@gmail.com>

ENV PHP_HOST phpfpm
ENV PHP_PORT 9000
ENV APP_MAGE_MODE default

COPY ./conf/nginx.conf /etc/nginx/
COPY ./conf/default.conf /etc/nginx/conf.d/
COPY ./bin/start.sh /usr/local/bin/start.sh

WORKDIR /srv/www

CMD ["/usr/local/bin/start.sh"]
