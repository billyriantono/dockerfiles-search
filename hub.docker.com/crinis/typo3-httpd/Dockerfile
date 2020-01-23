FROM httpd:2.4-alpine

ENV SERVER_ADMIN_EMAIL="you@example.com" \
    PHP_FPM="php:9000"

RUN apk add --no-cache nano tzdata && \
    mkdir -p /var/www/html/ && \
    chown www-data:www-data "/var/www/html"

COPY httpd-vhosts.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf

RUN sed -i '/LoadModule proxy_module/s/#//g' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/LoadModule proxy_fcgi_module/s/#//g' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/LoadModule expires_module/s/#//g' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/LoadModule rewrite_module/s/#//g' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/LoadModule vhost_alias_module/s/#//g' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/Include conf\/extra\/httpd-vhosts.conf/s/#//g' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/User daemon/c\User www-data' /usr/local/apache2/conf/httpd.conf && \
    sed -i '/Group daemon/c\Group www-data' /usr/local/apache2/conf/httpd.conf

WORKDIR /var/www/html/
