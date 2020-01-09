###################################
# Dockerfile for c++7 image proce-#
#  ssing in Linux environment     #
# BigDataEurope, Horizon2020      #
#                                 #
# gdal 2.2.2                      #
###################################

FROM gioargyr/iplcppcmake:1.0.0

MAINTAINER Giorgos Argyriou <gioargyr@gmail.com>

## INSTALLATION OF gdal 2.2.2
RUN wget --directory-prefix=/downloads http://download.osgeo.org/gdal/2.2.2/gdal-2.2.2.tar.gz \
 && cd /downloads \
 && tar -xzvf gdal-2.2.2.tar.gz \
 && cd /downloads/gdal-2.2.2 \
 && ./configure CC=/usr/bin/gcc-7 CXX=/usr/bin/g++-7 \
 && make -j4 \
 && make install

RUN cp /usr/local/lib/libgdal.so.20 /usr/lib/ \
 && gdalinfo --version \

RUN rm -rf /downloads/*
