FROM alpine

MAINTAINER Bartuer "bartuer@gmail.com"
RUN apk update; \
    apk add nginx;

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
