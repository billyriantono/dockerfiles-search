FROM openresty/openresty:1.11.2.5-alpine

EXPOSE 80 8000 8080 3000 3001 4000 5000

ADD nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

RUN chgrp -R 0 /usr/local/openresty/nginx/ && \
    chmod -R g=u /usr/local/openresty/nginx/
