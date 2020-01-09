FROM alpine:3.8

LABEL name="festival_tmp"
LABEL maintainer="Lukáš Dorňák <lukasdornak@gmail.com>"

RUN apk update; \
    apk add nginx

COPY . /var/www/festival/

COPY fest_nginx.conf /etc/nginx/conf.d/fest_nginx.conf

RUN mkdir -p /run/nginx \
    && rm /etc/nginx/conf.d/default.conf

EXPOSE 80

ENTRYPOINT nginx && /bin/ash
