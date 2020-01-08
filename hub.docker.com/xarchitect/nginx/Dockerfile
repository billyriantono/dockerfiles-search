FROM nginx:1.17

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y gettext-base
COPY nginx.vh.conf.tpl /root/nginx.vh.conf.tpl
RUN mkdir /var/log/nginx/log/

ENTRYPOINT envsubst '$NODE_HTTP_ENTRYPOINT$SITE_PORT$SITE_HOST$FASTCGI_PATH$SITE_ROOT$FASTCGI_READ_TIMEOUT$LOCATION$LOCATION_TRY_PATH$LOCATION_REWRITE_LAST' < /root/nginx.vh.conf.tpl > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'
