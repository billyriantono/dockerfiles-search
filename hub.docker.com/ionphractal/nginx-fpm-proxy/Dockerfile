FROM nginx:alpine
MAINTAINER Michael Both <both.michael@googlemail.com>
LABEL image="ionphractal/nginx-fpm-proxy" \
  version="0.1.0" \
  description="Nginx container to proxy to fpm."

ENV DEBIAN_FRONTEND="noninteractive"

RUN apk add --no-cache bash dumb-init \
 && deluser xfs \
 && addgroup -g 33 www-data \
 && adduser -S -D -H -u 33 -s /sbin/nologin www-data www-data \
 && mkdir -p /run/nginx /var/www/html \
 && chown -R www-data: /var/cache/nginx /run/nginx

ADD entrypoint.sh /
ADD nginx /etc/nginx
RUN chown -R www-data: /etc/nginx

WORKDIR /var/www
USER www-data
CMD ["dumb-init", "bash", "/entrypoint.sh"]
