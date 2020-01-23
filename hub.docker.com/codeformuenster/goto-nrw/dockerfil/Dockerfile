FROM postgres:alpine

RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main libcrypto1.1 \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing postgis
RUN ln -s /usr/share/postgresql/extension/* /usr/local/share/postgresql/extension/; exit 0
RUN ln -s /usr/lib/postgresql/* /usr/local/lib/postgresql/; exit 0

COPY initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
