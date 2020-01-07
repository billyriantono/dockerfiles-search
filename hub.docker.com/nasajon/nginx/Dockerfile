FROM alpine:3.6
MAINTAINER Nasajon<devops@nasason.com.br>

RUN apk add -U --no-cache \
    ca-certificates \
    nginx

COPY conf/nginx.conf /etc/nginx/
COPY conf/default.conf /etc/nginx/conf.d/

RUN mkdir -p /var/www/logs/nginx && \
    mkdir -p /tmp/nginx && \
    chown nginx /tmp/nginx

EXPOSE 80 443