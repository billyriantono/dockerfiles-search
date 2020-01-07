FROM alpine:latest

RUN apk add --update nginx --no-cache; \
    adduser -D -u 1000 -g 'www' www; \
    mkdir /www; \
    mkdir -p /var/lib/nginx; \
    chown -R www:www /var/lib/nginx; \
    chown -R www:www /www ; \
    mkdir /run/nginx

EXPOSE 80 443

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
