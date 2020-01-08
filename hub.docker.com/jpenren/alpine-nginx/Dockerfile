FROM alpine:latest

MAINTAINER Javier Pena

RUN apk add --update nginx && \
    rm -rf /var/cache/apk/*

COPY conf/ /etc/nginx/
COPY html/ /usr/share/nginx/html

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
