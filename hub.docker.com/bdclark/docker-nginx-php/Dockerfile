FROM bdclark/nginx-consul

ENV NGINX_LISTEN_PORT 80
ENV NGINX_ROOT_DIR /srv/web
ENV PHP_FPM_LISTEN_PORT 9000
ENV PHP_APP_TYPE php

COPY templates/* /etc/nginx/templates-available/
COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
