FROM nginx

MAINTAINER lvyalin "lvyalin.yl@gmail.com"

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.vh.www.conf /etc/nginx/conf.d/www.conf
COPY fastcgi_params /etc/nginx/fastcgi_params

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]