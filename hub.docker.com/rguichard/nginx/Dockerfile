FROM alpine:3.1

MAINTAINER Romain Guichard <rguichard@vsense.fr>

RUN apk --update add \
    nginx \
    git \
    supervisor \
    php-fpm
RUN deluser nginx && \
    adduser -D -u 7001 -s /sbin/nologin -h /var/www nginx && \
    mkdir -p /tmp/nginx/client-body && \
    sed -i \
    -e 's/group =.*/group = nginx/' \
    -e 's/user =.*/user = nginx/' \
    -e 's/listen\.owner.*/listen\.owner = nginx/' \
    -e 's/listen\.group.*/listen\.group = nginx/' \
    -e 's/error_log =.*/error_log = \/dev\/stdout/' \
    /etc/php/php-fpm.conf \
    && sed -i \
    -e '/open_basedir =/s/^/\;/' \
    /etc/php/php.ini

COPY supervisord.conf /etc/supervisord.conf
COPY supervisord-nginx-php.ini /etc/supervisor.d/supervisord-nginx-php.ini
COPY nginx.conf /etc/nginx/nginx.conf
COPY consul-template /usr/bin/consul-template

WORKDIR /etc/nginx

EXPOSE 80 443

CMD ["supervisord", "-c", "/etc/supervisord.conf", "-n"]
