FROM php:fpm-alpine
MAINTAINER bulzipke <bulzipke@naver.com>

RUN apk update && apk upgrade
COPY scripts/* /root/

VOLUME /var/www/html

EXPOSE 9000

CMD ["/root/setup.sh"]

