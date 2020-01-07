FROM spacetimeanalytics/python-gdal
MAINTAINER Space Time Analytics <devs@spacetimeanalytics.com>

RUN apt-get update -yqq
RUN apt-get install -yqq software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update -yqq
RUN apt-get install -yqq gcc-7 g++-7 git python zlib1g-dev make pkg-config curl
RUN apt-get install -yqq libicu-dev \
    python-dev libxml2 libxml2-dev \
    libfreetype6 libfreetype6-dev \
    libjpeg-dev \
    libpng-dev \
    libproj-dev \
    libtiff-dev \
    libcairo2 libcairo2-dev python-cairo python-cairo-dev \
    libcairomm-1.0 libcairomm-1.0-dev \
    ttf-unifont ttf-dejavu ttf-dejavu-core ttf-dejavu-extra \
    git build-essential python-nose python-gdal \
    libsqlite3-dev
RUN apt-get install -yqq libboost-dev libboost-filesystem-dev libboost-program-options-dev libboost-python-dev libboost-regex-dev libboost-system-dev libboost-thread-dev
ENV PYTHON=python2
RUN git clone --branch gdal_vsi https://github.com/spacetimeanalytics/mapnik /tmp/mapnik
RUN cd /tmp/mapnik && git submodule update --init
ENV SHELL=/bin/bash
RUN apt-get install -yqq libharfbuzz-dev
ADD build.sh /tmp
RUN /tmp/build.sh

RUN git clone --branch v3.0.x https://github.com/spacetimeanalytics/python-mapnik.git /tmp/mapnik-python
RUN cd /tmp/mapnik-python && python setup.py install

