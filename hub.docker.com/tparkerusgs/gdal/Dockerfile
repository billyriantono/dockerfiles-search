FROM gcc:6 AS gdal
WORKDIR /build
RUN  curl -fsSLO http://download.osgeo.org/gdal/2.2.0/gdal-2.2.0.tar.gz 
RUN gzip -dc gdal-2.2.0.tar.gz | tar xf -
WORKDIR /build/gdal-2.2.0 
RUN ./configure
RUN make
RUN make install 
