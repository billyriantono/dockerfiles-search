FROM nginx:alpine

LABEL name=zrhoffman/drupal-nginx:dev version=0.0.0

RUN set -o errexit -o nounset -o pipefail;\
    apk add --no-cache openssl;\
\
    #Add nginx to the www-data group so we can use the PHP container's FPM
    #socket
    addgroup nginx www-data;\
\
    mkdir /app;

COPY ./etc /etc
EXPOSE 80 443

CMD set -o errexit -o nounset -o pipefail;\
    cd /etc/nginx/ssl;\
    openssl req\
        -new -x509\
        -newkey rsa:4096\
        -nodes\
        -out site.crt\
        -keyout site.key\
        -subj "/C=US/ST=Colorado/L=Denver/O=Organization/CN=*";\
    cd -;\
\
    exec /usr/sbin/nginx;
