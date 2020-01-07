FROM nginx:1.12
MAINTAINER Yannick Vanhaeren

RUN set -ex \
    && sed -i -e "s|keepalive_timeout\s*65|keepalive_timeout 2|" /etc/nginx/nginx.conf \
    && sed -i -e "s|#gzip\s*on;|gzip on;\n\tgzip_disable \"msie6\";\n\tgzip_types text/plain application/xml;|" /etc/nginx/nginx.conf
