FROM postgres:11.4

LABEL maintainer="Ignacio Fernandez Dussaut <Ignacio.Dussaut@Cartesian.com>" \
  description="Based images for PostgreSQL Database with PostGIS extension"

ENV POSTGIS_VERSION 2.5.2
ENV POSTGIS_SHA256 b6cb286c5016029d984f8c440947bf9178da72e1f6f840ed639270e1c451db5e

ADD http://download.osgeo.org/postgis/source/postgis-${POSTGIS_VERSION}.tar.gz /usr/src/postgis/
ADD resources/build.sh /usr/src/postgis/

RUN chmod 777 /usr/src/postgis/build.sh && /usr/src/postgis/build.sh

COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
