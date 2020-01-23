FROM alpine:3.3

MAINTAINER Harry Danes <docker@hdanes.nl>

RUN apk update && \
  apk upgrade && \
  apk add php-fpm && \
  rm -rf /var/cache/apk/*

RUN sed -i '/^listen/c listen = 0.0.0.0:9000' /etc/php/php-fpm.conf && \
  sed -i 's/^expose_php = On/expose_php = Off/' /etc/php/php.ini

RUN mkdir -p /var/www

VOLUME /var/www

EXPOSE 9000

ENTRYPOINT ["php-fpm", "-F"]
