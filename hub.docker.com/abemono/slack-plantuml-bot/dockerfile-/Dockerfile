FROM abc3660170/osm2pgsql:latest
RUN yum install nodejs gdal -y
RUN npm install carto -g
WORKDIR /home
RUN git clone -b v2.27.0 https://github.com/gravitystorm/openstreetmap-carto.git
WORKDIR /home/openstreetmap-carto
RUN ./get-shapefiles.sh
RUN rm -rf data/*.zip
RUN rm -rf data/*.tgz
RUN sed -i "s/\"dbname\": \"gis\"/\"dbname\": \"osm\",\n\t\"user\":\"btf\",\n\t\"password\":\"123456\",\n\t\"host\":\"127.0.0.1\",\n\t\"port\":\"5432\"/g" /home/openstreetmap-carto/project.mml
RUN carto project.mml > mapnik.xml
