FROM chentung/base:latest
LABEL maintainer="chentung <chentung.wu@outlook.com>"

COPY entrypoint.sh /entrypoint.sh

RUN apk add --update nginx \
    && chmod a+x /entrypoint.sh \
    && echo 'hello world' > /var/www/index.html \
    && rm -rf /var/cache/apk/*

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80 443

ENTRYPOINT ["/entrypoint.sh"]
