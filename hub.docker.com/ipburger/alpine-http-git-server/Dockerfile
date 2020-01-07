FROM nginx:stable-alpine

MAINTAINER Vitor Boufleur "vboufleur@ipburger.com"

RUN apk add --no-cache git-daemon fcgiwrap spawn-fcgi

COPY nginx.conf /etc/nginx/nginx.conf.template

VOLUME ["/git"]

EXPOSE 80

CMD spawn-fcgi -s /run/fcgi.sock /usr/bin/fcgiwrap && \
    envsubst '\${SERVER_NAME}' < /etc/nginx/nginx.conf.template > /etc/nginx/nginx.conf && \
    nginx -g "daemon off;"
