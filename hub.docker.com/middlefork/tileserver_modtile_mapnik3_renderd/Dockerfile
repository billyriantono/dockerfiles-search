FROM middlefork/baseimage

#2018-10-16 working.

RUN apt update \
 && apt install -y \
  systemd \
  autoconf build-essential libtool \
  apache2 apache2-dev \
  git \
  python3 \
  munin \
  mapnik3.0 libmapnik-dev python3-mapnik mapnik-utils \
  supervisor


# Install mod_tile and renderd
WORKDIR /tmp
RUN git clone --depth 1 https://github.com/middlefork/mod_tile.git \
 && cd mod_tile \
 && ./autogen.sh \
 && ./configure \
 && make \
 && make install \
 && make install-mod_tile \
 && ldconfig


# copy configuration files
WORKDIR /tmp/mod_tile
RUN cp -p debian/tile.load /etc/apache2/mods-available \
  && cp -p readme.txt /usr/share/doc/libapache2-mod-tile \
  && cp -p munin/mod_tile* /usr/share/munin/plugins \
  && cp -p openstreetmap-tiles-update-expire /usr/bin/ \
  && cp -p osmosis-db_replag /usr/bin \
  && cp -p slippymap.html /var/www/osm \
  && cp debian/renderd.conf /etc \
  && cd / && rm -rf /tmp/mod_tile

COPY tileserver_site.conf /etc/apache2/sites-available

# Enable mod_tile
RUN a2enmod tile \
  && a2enmod headers \
  && a2dissite 000-default \
  && a2ensite tileserver_site.conf \
  && service apache2 restart

# Setup and run renderd
RUN mkdir /var/run/renderd \
 && chown www-data:www-data /var/run/renderd \
 && mkdir /var/lib/mod_tile \
 && chown www-data:www-data /var/lib/mod_tile \
 && chmod a+wrx /var/lib/mod_tile \
 && /usr/local/bin/renderd -c /etc/renderd.conf \
 && mkdir -p /data/osm


# build the map style sheet (using nodejs and npm)
WORKDIR /data/osm
RUN npm install -g carto \
 && git clone --depth 1 https://github.com/gravitystorm/openstreetmap-carto.git \
 && cd openstreetmap-carto \
 # we like the OSM db to be named 'osm', not 'gis'
 && sed -i 's/dbname: "gis"/dbname: "osm"/g' project.mml \
 # problems with coalesce function
 && sed -i "s/COALESCE(layer,0)/COALESCE\(layer,'0')/g" project.mml \
 && sed -i "s/COALESCE(layer, 0)/COALESCE\(layer,'0')/g" project.mml \
 && carto project.mml > osm-mapnik.xml

COPY get-osm-shapes /usr/local/bin
RUN chmod a+x /usr/local/bin/get-osm-shapes

EXPOSE 80
COPY supervisord.conf /etc/supervisor/conf.d
CMD ["/usr/bin/supervisord"]



