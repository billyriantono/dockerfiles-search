FROM postgres:11.6

ENV POSTGIS_MAJOR 2.5
ENV POSTGIS_VERSION 2.5.3+dfsg-2.pgdg90+1
ENV PACKAGE_POSTGIS_VERSION 3.0.0+dfsg-2~exp1.pgdg90+1
RUN \
  apt-get update && \
  apt-cache showpkg postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR && \
  apt-get install -y --no-install-recommends \
    postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR=$POSTGIS_VERSION \
    postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR-scripts=$POSTGIS_VERSION \
    postgis=$PACKAGE_POSTGIS_VERSION && \
  rm -rf /var/lib/apt/lists/*
