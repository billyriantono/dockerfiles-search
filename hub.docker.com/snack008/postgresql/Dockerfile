FROM postgres:9.3-alpine

MAINTAINER srsergey.ivanenko@gmail.com

RUN apk add --no-cache \
     --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
     --repository http://dl-cdn.alpinelinux.org/alpine/edge/main \
    nano vim wget git openssl \
    gcc g++ make \
    autoconf \
    automake \
    json-c \
    libtool \
    libxml2-dev \
    libxslt \
    gdal-dev \
    geos-dev \
    proj4-dev \
    protobuf-c-dev \
    geos \
    gdal \
    proj4 \
    protobuf-c \
    perl

RUN cd /var/tmp && git clone --single-branch -b 5.2.0 https://github.com/OSGeo/PROJ.git proj4 \
    && cd /var/tmp/proj4 \
    && ./autogen.sh \
    && ./configure \
    && make \
    && make install

RUN cd /var/tmp && git clone --single-branch -b 2.1.2 https://github.com/blac3kman/postgis.git postgis-2.1.2 \
    && cd /var/tmp/postgis-2.1.2 \
    && ./autogen.sh \
    && ./configure \
    && make \
    && make install

RUN apk del gcc g++ make autoconf automake  wget git \
    && rm -rf /var/tmp/* /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apk/*

COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY ./update-postgis.sh /usr/local/bin