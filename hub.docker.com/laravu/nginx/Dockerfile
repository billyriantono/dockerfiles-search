FROM nginx:alpine

LABEL maintainer="4ngo.ru@gmail.com"
LABEL version="0.4.0"
LABEL description="Nginx for LaraVu"

ADD conf/ /etc/nginx/

ARG PHP_UPSTREAM=php

# fix a problem--#397, change application source from dl-cdn.alpinelinux.org to aliyun source.
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

RUN apk add --update --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data \
    && rm /etc/nginx/conf.d/default.conf
#     \
#    && echo "upstream php-upstream { server ${PHP_UPSTREAM}:9000; }" > /etc/nginx/conf.d/upstream.conf

CMD ["nginx"]

EXPOSE 80 443
