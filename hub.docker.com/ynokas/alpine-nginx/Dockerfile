FROM nginx:alpine

ADD vhost.conf /etc/nginx/conf.d/default.conf
RUN set -x \
    && addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data
