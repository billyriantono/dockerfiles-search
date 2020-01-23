FROM alpine:latest

LABEL maintainer="Alex Povyshev"

RUN apk update && \
  apk add wget nginx php7 php7-common php7-mbstring php7-session php7-json php7-fpm && \
  wget -q http://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz -P /tmp && \
  mkdir /var/www/dokuwiki && \
  tar -xzf /tmp/dokuwiki-stable.tgz -C /var/www/dokuwiki --strip-components 1 && \
  chown -R nginx:nginx /var/www/dokuwiki && \
  chmod -R 777 /var/www/dokuwiki

COPY nginx/sites/default /etc/nginx/conf.d/default.conf

RUN mkdir /run/nginx/ && touch /run/nginx/nginx.pid && \
  touch /var/log/nginx/access.log && touch /var/log/nginx/error.log

COPY entrypoint.sh /entrypoint.sh

EXPOSE 80

CMD ["sh", "/entrypoint.sh"]
