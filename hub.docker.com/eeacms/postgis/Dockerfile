FROM eeacms/postgres:9.6-3.4

MAINTAINER michimau <mauro.michielon@eea.europa.eu>

ENV POSTGIS_MAJOR 2.4

RUN apt-get update \
      && apt-get install -y --no-install-recommends \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts \
           vim \
           ca-certificates \
      && rm -rf /var/lib/apt/lists/*


RUN mkdir -p /docker-entrypoint-initdb.d
#keep initdb-postgis.sh as not executable!
COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY ./create_ssl_files.sh /

RUN sed -i -e 's/exec "$@"/sh \/create_ssl_files.sh \&\nexec "$@"/g' /master-entrypoint.sh

COPY conf/ssl.conf /postgresql.conf.d/

RUN mkdir -p /var/ssl && \
    chown -R postgres.postgres /var/ssl
