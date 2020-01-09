FROM nmhung1210/nginx-alpine-amplify:1.0.0

LABEL maintainer="Robert Pham <kingdom102@gmail.com>"

ENV NGINX_FPM_AMPLIFY_VERSION 1.0.0

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
        php7 \
        php7-fpm \
        php7-opcache \
        php7-gd \
        php7-mysqli \
        php7-zlib \
        php7-zip \
        php7-curl \
        php7-openssl \
        php7-pdo_mysql \
        php7-pdo \
        php7-mcrypt

VOLUME [ "/usr/share/etc/nginx", "/usr/share/etc/php7", "/var/www/html" ]

EXPOSE 80 443

STOPSIGNAL SIGTERM

COPY conf.d/nginx /etc/nginx
COPY conf.d/php7 /etc/php7

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT []
CMD ["/entrypoint.sh"]