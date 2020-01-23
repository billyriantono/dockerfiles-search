FROM openresty/openresty:1.11.2.5-alpine

EXPOSE 8080
ADD nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

RUN adduser -D -u 1000 nginx && \
    chgrp -R 1000 /usr/local/openresty/nginx/ && \
    chmod -R g=u /usr/local/openresty/nginx/

USER 1000

