FROM nerelohw/docker-alpine

RUN echo "@edge_main http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories
RUN echo "@edge_testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk add --no-cache --update su-exec@edge_main \
    gosu@edge_testing \
    pwgen@edge_main \
    libedit@edge_main \
    libpq@edge_main \
    tzdata@edge_main \
    postgresql-client@edge_main \
    postgresql@edge_main \
    postgresql-contrib@edge_main && \
    mkdir /docker-entrypoint-initdb.d && \
    cp /usr/share/zoneinfo/America/New_York /etc/localtime && \
    mkdir /run/postgresql && \
    mkdir /var/run/postgresql && \
    mkdir /etc/postgresql && \
    chown postgres:postgres /run/postgresql && \
    chown postgres:postgres /var/run/postgresql && \
    chown postgres:postgres /etc/postgresql && \
    rm -rf /var/cache/apk/*

ENV LANG en_US.UTF-8
ENV PGDATA /var/lib/postgresql/data
VOLUME /var/lib/postgresql

COPY rootfs/_usr_local_bin_docker-entrypoint.sh /docker-entrypoint.sh
COPY tmpl/_etc_postgresql_postgresql.conf /etc/postgresql/postgresql.conf
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres","-c","config_file=/etc/postgresql/postgresql.conf"]
#https://github.com/wodby/postgres/tree/master/action
