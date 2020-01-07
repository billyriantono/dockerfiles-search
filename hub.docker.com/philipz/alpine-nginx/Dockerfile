FROM alpine:latest
MAINTAINER Philipz <philipzheng@gmail.com>

RUN apk --update add nginx && \
    rm -rf /var/cache/apk/*

COPY nginx.conf /etc/nginx/nginx.conf

VOLUME ["/usr/share/nginx/html","/var/log/nginx","/etc/nginx/conf.d"]

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
