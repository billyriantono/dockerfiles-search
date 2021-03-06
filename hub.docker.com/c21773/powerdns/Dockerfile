FROM alpine:3.7
MAINTAINER Cristian Müller <cristian.mueller@muber.de>

ENV REFRESHED_AT="2018-07-15" \
    POWERDNS_VERSION=4.1.3 \
    MYSQL_AUTOCONF=false \
    MYSQL_HOST="mysql" \
    MYSQL_PORT="3306" \
    MYSQL_USER="root" \
    MYSQL_PASS="root" \
    MYSQL_DB="pdns"

RUN apk --update add \
          libstdc++ libgcc libressl libsodium boost-program_options \
          mysql-client mariadb-client-libs mariadb-libs \
          libpq postgresql-libs \
          sqlite-libs lua && \
        apk add --virtual build-deps \
          file g++ make mariadb-dev postgresql-dev sqlite-dev lua-dev libressl-dev boost-dev libsodium-dev curl && \
    curl -sSL https://downloads.powerdns.com/releases/pdns-$POWERDNS_VERSION.tar.bz2 | tar xj -C /tmp && \
    cd /tmp/pdns-$POWERDNS_VERSION && \
    ./configure --prefix="" --exec-prefix=/usr --sysconfdir=/etc/pdns \
      --with-modules="bind gmysql gpgsql gsqlite3" --with-dynmodules="pipe random lua remote" && \
    make && make install-strip && cd / && \
    mkdir -p /etc/pdns/conf.d && \
    addgroup -S pdns 2>/dev/null && \
    adduser -S -D -H -h /var/empty -s /bin/false -G pdns -g pdns pdns 2>/dev/null && \
    apk del --purge build-deps && \
    rm -rf /tmp/pdns-$POWERDNS_VERSION /var/cache/apk/*

ADD schema.sql pdns.conf /etc/pdns/
ADD entrypoint.sh /

EXPOSE 53/tcp 53/udp

ENTRYPOINT ["/entrypoint.sh"]
