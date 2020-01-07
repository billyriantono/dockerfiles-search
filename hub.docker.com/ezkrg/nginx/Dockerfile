FROM alpine:3.4

RUN addgroup -S www-data \
 && adduser -D -S -G www-data -s /usr/sbin/nologin -h /var/www www-data \
 && apk add --no-cache --update nginx

COPY nginx.conf /etc/nginx/nginx.conf
COPY docker-entrypoint.sh /usr/local/bin/

EXPOSE 80 443

ENTRYPOINT [ "docker-entrypoint.sh" ]

CMD [ "nginx", "-g", "daemon off;" ]
