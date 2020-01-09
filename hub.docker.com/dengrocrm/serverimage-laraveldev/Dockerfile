FROM dengrocrm/serverimage-laravel:latest
MAINTAINER dandengro
LABEL maintainer="dandengro"

RUN \
    # install runtime packages
    apk add --no-cache \
        php7-pdo_sqlite \
        php7-sqlite3 \
        php7-xdebug \
        redis \
        sqlite \
    # # cleanup
    && rm -rf \
        /tmp/*

# Copy local files
COPY root/ /

# Expose ports.
EXPOSE 80 443

ENTRYPOINT ["/init"]
