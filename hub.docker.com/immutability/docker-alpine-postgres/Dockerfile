FROM alpine

RUN echo "@edge http://nl.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories
RUN apk update
RUN apk add curl "libpq@edge<9.7" "postgresql-client@edge<9.7" "postgresql@edge<9.7" "postgresql-contrib@edge<9.7"
RUN mkdir /docker-entrypoint-initdb.d
RUN curl -o /usr/local/bin/gosu -sSL "https://github.com/tianon/gosu/releases/download/1.2/gosu-amd64"
RUN chmod +x /usr/local/bin/gosu
RUN apk del curl
RUN mkdir -p /run/postgresql
RUN chown -R postgres:postgres /run/postgresql
RUN rm -rf /var/cache/apk/*

ENV LANG en_US.utf8
ENV PGDATA /var/lib/postgresql/data
VOLUME /var/lib/postgresql/data

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
