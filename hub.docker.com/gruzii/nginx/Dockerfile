FROM gliderlabs/alpine:latest

EXPOSE 80 443

RUN apk-install nginx \
    && mkdir -p /tmp/nginx/client-body

COPY ./nginx.conf /etc/nginx/nginx.conf

VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d"]

WORKDIR /etc/nginx

CMD ["nginx", "-g", "daemon off;"]




WORKDIR /tmp
