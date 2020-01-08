FROM postgres:10
LABEL maintainer="Denis Krivak"

ENV POSTGIS_MAJOR 2.4

RUN apt update && \
    apt install -y \
        postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR \
        postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts \
        postgis && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /docker-entrypoint-initdb.d
COPY ./init.sh /docker-entrypoint-initdb.d/postgis.sh
