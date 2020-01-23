FROM abc3660170/pg:latest
WORKDIR /usr/local/src
RUN git clone git://github.com/openstreetmap/osm2pgsql.git
RUN yum install cmake gcc-c++ boost-devel expat-devel zlib-devel bzip2-devel postgresql-devel geos-devel proj-devel proj-epsg lua-devel postgresql95-devel -y
WORKDIR /usr/local/src/osm2pgsql
RUN mkdir build
WORKDIR /usr/local/src/osm2pgsql/build
RUN cmake ..
RUN make
RUN make install
RUN osm2pgsql -version; exit 0
RUN rm -rf /usr/local/src/osm2pgsql

