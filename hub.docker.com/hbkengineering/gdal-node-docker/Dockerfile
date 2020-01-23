FROM node:8

# This image provides a Node.JS environment you can use to run your Node.JS
# applications.

MAINTAINER HBK Engineering, LLC <apps@hbkengineering.com>

RUN apt-get update && apt-get install -y --no-install-recommends psmisc build-essential "libpng-dev" libtiff5 libkml-dev zlib1g-dev && rm -rf /var/lib/apt/lists/*

# Install proj4 as a prerequisite for GDAL
WORKDIR /etc/proj4
RUN wget http://download.osgeo.org/proj/proj-4.9.3.tar.gz

RUN tar -zxvf proj-4.9.3.tar.gz
WORKDIR proj-4.9.3

RUN ./configure
RUN make
RUN make install
# End proj4 install #

# Install gdal/ogr2ogr
WORKDIR /etc/gdal
RUN wget http://download.osgeo.org/gdal/2.1.3/gdal-2.1.3.tar.gz

RUN tar -zxvf gdal-2.1.3.tar.gz
WORKDIR gdal-2.1.3

RUN ./configure --with-static-proj4=/usr/local/lib --with-threads --with-libtiff=internal --with-geotiff=internal --with-jpeg=internal --with-gif=internal --with-png=internal --with-libz=internal --with-libkml
RUN make
RUN make install

RUN ln -s /usr/local/bin/ogr2ogr /usr/local/ogr2ogr
RUN ldconfig
WORKDIR /opt/app-root/src
# End ogr2ogr install

CMD gdalinfo --version && gdalinfo --formats && ogrinfo --formats
