FROM python:3.6-alpine

ENV SPATIALITE_LIBRARY_PATH "/usr/lib/mod_spatialite.so.7"
ENV GEOS_LIBRARY_PATH "/usr/lib/libgeos_c.so.1"
ENV GDAL_LIBRARY_PATH "/usr/lib/libgdal.so.20"

RUN set -ex \
    && apk add --no-cache --virtual .tools \
      gettext \
    && apk add --no-cache --virtual .geo \
      --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
      geos \
      proj4 \
      gdal \
      libspatialite \
    && ln -s /usr/lib/libproj.so.12 /usr/lib/libproj.so
