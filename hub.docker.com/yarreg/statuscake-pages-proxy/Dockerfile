FROM nginx:1.14.0-alpine

COPY default.conf /etc/nginx/conf.d/default.conf.tmp
COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]