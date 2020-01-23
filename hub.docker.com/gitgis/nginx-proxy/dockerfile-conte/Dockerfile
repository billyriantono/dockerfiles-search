FROM postgres:9.3
MAINTAINER Zacharias Knudsen <zacharias@gisgroup.dk>

ENV POSTGIS_MAJOR 2.1

RUN echo deb http://http.debian.net/debian wheezy-backports main >> /etc/apt/sources.list
RUN apt-get update \
      && apt-get install -y --no-install-recommends \
           postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR \
           postgis \
      && rm -rf /var/lib/apt/lists/*

# parent mounts /var/lib/postgresql/data as volume and exposes 5432
