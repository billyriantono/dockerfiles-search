FROM php:7.1.4-fpm-alpine

ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/docker-entrypoint.sh"]
CMD ["/usr/local/sbin/php-fpm"]

RUN apk add --no-cache \
    tini

COPY bin/ /usr/local/bin/
COPY docker-entrypoint.d/ /etc/docker-entrypoint.d/

RUN rm -rf /var/www/html
COPY app/* /var/www/
