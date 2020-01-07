FROM croudtech/base:latest

# NGINX INSTALLATION

RUN set -x \
 && apk update \
 && apk add --update nginx

VOLUME /var/www/app

EXPOSE 80
EXPOSE 443

ENV DOLLAR=$
ENV NGINX_HOST localhost
ENV NGINX_PORT 80
ENV DOC_ROOT /var/www/app
ENV PHP_FPM_HOST 127.0.0.1

USER root

COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/default.conf.template /etc/nginx/conf.d/app.conf.template
COPY config/nginx-supervisor.ini /etc/supervisor.d/nginx.ini
COPY docker-nginx-entrypoint.sh /etc/container_start_scripts/
RUN chmod +x /etc/container_start_scripts/docker-nginx-entrypoint.sh

