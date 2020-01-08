FROM postgres:9.4.4
MAINTAINER Ryan Peterson <ryan.m.peterson@gmail.com>

# get deps
RUN apt-get update \
  && apt-get install -y wget \
  && apt-get install -y unzip \
  && apt-get install -y make gcc \
  && apt-get install -y libxml2-dev libgeos-dev libproj-dev libgdal-dev libpcre3-dev \
  && apt-get install -y libpq-dev postgresql-server-dev-9.4

# fetch postgis
RUN wget http://postgis.net/stuff/postgis-2.2.1dev.tar.gz \
  && tar -xvzf postgis-2.2.1dev.tar.gz \
  && rm -f postgis-2.2.1dev.tar.gz

# make/install postgis
RUN cd /postgis-2.2.1dev && ./configure && make install && ldconfig

# cleanup apt-get
RUN apt-get clean \
  && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

ADD init/ docker-entrypoint-initdb.d/

