FROM opsat/base:latest

MAINTAINER "Serban TEODORESCU <teodorescu.serban@gmail.com>"

COPY run_nginx /

RUN apk add --update-cache nginx && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /etc/nginx /etc/services.d/nginx /run/nginx && \
    mv /run_nginx /etc/services.d/nginx/run

EXPOSE 6379

VOLUME /var/log/nginx /var/cache/redis /var/www
