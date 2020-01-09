FROM openresty/openresty:alpine-fat
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

RUN adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 nginx && \
    apk add --no-cache libldap && \
    apk add --no-cache --virtual .build-deps openldap-dev && \
    luarocks-5.1 install lualdap && \
    apk del .build-deps

ENTRYPOINT ["/usr/local/openresty/bin/openresty"]
