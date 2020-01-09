FROM postgres:10.3

ENV POSTGIS_MAJOR 2.4
ENV POSTGIS_VERSION 2.4.4

# Per postgres best practices
ENV PGDATA=/var/lib/postgresql/data/pgdata

RUN apt-get update \
      && apt-cache showpkg postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR \
      && apt-get install -y --no-install-recommends \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts \
           postgis \
      && rm -rf /var/lib/apt/lists/*

# Add unaccent extension
RUN mkdir -p /docker-entrypoint-initdb.d && \
    echo "CREATE EXTENSION unaccent;" >  /docker-entrypoint-initdb.d/unaccent.sql

COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY ./update-postgis.sh /usr/local/bin

# Non root for security
RUN usermod -u 1000 postgres && \
    groupmod -g 1000 postgres && \
    chown -R postgres:postgres /var/lib/postgresql

USER 1000