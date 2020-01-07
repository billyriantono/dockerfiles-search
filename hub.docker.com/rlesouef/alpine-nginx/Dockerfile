FROM alpine:latest
MAINTAINER Open Source Services [os2.fr]

RUN apk add --update \
    bash nano nginx && \
    rm -rf /var/cache/apk/*

RUN adduser www-data -G www-data -H -s /bin/false -D

COPY src/ .

EXPOSE 80 443

VOLUME ["/var/www", "/var/log/nginx"]
WORKDIR /etc/nginx

CMD ["nginx"]
