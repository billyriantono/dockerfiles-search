FROM golang:1.12 AS compile_stage

LABEL maintainer="andreas.thomas@th-nuernberg.de"
LABEL name="tile-server"
LABEL version="0.1.0"

WORKDIR /

COPY ./scripts/*.go ./
RUN  go mod init tile_server

RUN env GOOS=linux go build -o /start /start.go


FROM node AS carto_stage

WORKDIR /
RUN git clone https://github.com/gravitystorm/openstreetmap-carto 
WORKDIR /openstreetmap-carto/
COPY project.mml project.mml
RUN npx carto project.mml > /mapnik.xml

FROM ubuntu:18.04

ENV DB_HOST X
ENV DB_PORT X
ENV DB_USER X
ENV DB_PASSWORD X
ENV DB_NAME X

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -qq update && apt-get -qq install -y --no-install-recommends \
		apache2 \
		apache2-dev \
		autoconf \
		ca-certificates \
		fonts-hanazono \
		fonts-noto-cjk \
		fonts-noto-hinted \
		fonts-noto-unhinted \
		g++ \
		gdal-bin \
		git \
		libbz2-dev \
		libgeos-dev \
		libgeos++-dev \
		libmapnik-dev \
		libproj-dev \
		libtool \
		libxml2-dev \
		mapnik-utils \
		python-mapnik \
		ttf-unifont \
		wget \
	&& apt-get -qq autoremove -y \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /
RUN git clone https://github.com/gravitystorm/openstreetmap-carto.git
COPY --from=carto_stage /mapnik.xml /openstreetmap-carto/mapnik.xml

# Install mod_tile

RUN git clone -b switch2osm https://github.com/SomeoneElseOSM/mod_tile.git
WORKDIR /mod_tile
RUN ./autogen.sh \
	&& ./configure \
	&& make -j "$(nproc)" \
	&& make -j "$(nproc)" install \
	&& make -j "$(nproc)" install-mod_tile \
	&& ldconfig

# Setting up webserver
COPY ./renderd.conf /usr/local/etc/renderd.conf

# Configure Apache
RUN mkdir -p /var/lib/mod_tile && mkdir -p /var/run/renderd
RUN echo "LoadModule tile_module /usr/lib/apache2/modules/mod_tile.so" >> /etc/apache2/conf-available/mod_tile.conf
RUN a2enconf mod_tile

COPY ./apache.conf /etc/apache2/sites-available/000-default.conf
RUN service apache2 start && service apache2 reload && service apache2 reload

EXPOSE	80
COPY --from=compile_stage /start /start



ENTRYPOINT [ "/start" ] 
 