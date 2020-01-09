FROM nginx:1.13.3
MAINTAINER Yohanes Pradono <doniking@gmail.com>

ENV PHP_HOST phpfpm
ENV PHP_PORT 9000
ENV APP_MAGE_MODE default

COPY ./conf/nginx.conf /etc/nginx/
COPY ./conf/default.conf /etc/nginx/conf.d/
COPY ./bin/start.sh /usr/local/bin/start.sh

WORKDIR /var/www/html

CMD ["bash", "/usr/local/bin/start.sh"]
