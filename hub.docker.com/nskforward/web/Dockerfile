FROM nskforward/php:7.2.11

RUN apk add --no-cache --update supervisor nginx
	
COPY php-fpm.conf /usr/local/etc/php-fpm.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY index.php /app/backend/index.php

RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

ENTRYPOINT supervisord -n -c /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80 443
