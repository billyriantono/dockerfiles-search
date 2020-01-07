FROM nginx:alpine-perl

ENV NGINX_CONF_FILE php
ENV NGINX_MAX_BODY_SIZE 200M
ENV NGINX_FASTCGI_PASS rshop-php:9000
ENV NGINX_WEBROOT /var/www/html/webroot
ENV NGINX_MEMCACHED rshop-memcached:11211
ENV NGINX_CACHE_PREFIX rshop-
ENV NGINX_IMAGINARY http://rshop-imaginary:9099

RUN addgroup -g 3000 -S rshop && adduser -u 3000 -S -G rshop rshop

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY rshop.d/* /etc/nginx/rshop.d/

EXPOSE 9020

CMD envsubst '\$NGINX_CONF_FILE \$NGINX_MAX_BODY_SIZE \$NGINX_FASTCGI_PASS \$NGINX_WEBROOT' < /etc/nginx/conf.d/default.conf > /etc/nginx/conf.d/default.conf \
    && envsubst '\$NGINX_CACHE_PREFIX' < /etc/nginx/rshop.d/memcached_key.conf > /etc/nginx/rshop.d/memcached_key.conf \
    && envsubst '\$NGINX_FASTCGI_PASS' < /etc/nginx/rshop.d/fpm_status.conf > /etc/nginx/rshop.d/fpm_status.conf \
    && envsubst '\$NGINX_FASTCGI_PASS \$NGINX_WEBROOT \$NGINX_MEMCACHED' < /etc/nginx/rshop.d/php_memcached.conf > /etc/nginx/rshop.d/php_memcached.conf \
    && envsubst '\$NGINX_FASTCGI_PASS \$NGINX_WEBROOT' < /etc/nginx/rshop.d/php.conf > /etc/nginx/rshop.d/php.conf \
    && envsubst '\$NGINX_IMAGINARY' < /etc/nginx/rshop.d/imaginary.conf > /etc/nginx/rshop.d/imaginary.conf \
    && nginx -g 'daemon off; load_module /etc/nginx/modules/ngx_http_perl_module-debug.so;'
