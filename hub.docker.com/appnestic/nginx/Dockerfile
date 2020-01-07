FROM appnestic/alpine

RUN apk-install nginx \
    && mkdir -p /tmp/nginx/client-body \
    && mkdir -p /var/www

ADD nginx.conf /etc/nginx/nginx.conf

WORKDIR /etc/nginx

EXPOSE 80 443

CMD ["nginx", "-g"]
