FROM debian:buster

RUN apt update \
 && apt install -y \
 fonts-hanazono \
 fonts-noto \
 git \
 libgdal20 \
 libjs-proj4 \
 libmapnik-dev \
 libmapnik3.0 \
 libmapserver-dev \
 libmapserver2 \
 mapnik-utils \
 mapnik-vector-tile \
 mapserver-bin \
 npm \
 osm2pgsql \
 postgis \
 postgis-gui \
 postgresql-11 \
 python3 \
 python3-gdal \
 python3-mapnik \
 python3-pip \
 ttf-unifont \
 && rm -rf /var/lib/apt/lists/*

# make python3 the default.
RUN unlink /usr/bin/python && ln -s /usr/bin/python3 /usr/bin/python

# Default CMD is bash, whoopie.
CMD bash
