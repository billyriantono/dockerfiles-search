FROM golang AS script_stage

# These will be overwritten by the docker-compose file
ENV DB_NAME X
ENV DB_HOST X
ENV DB_PASSWORD X
ENV DB_PORT X
ENV DB_USER X

WORKDIR /

COPY ./scripts/import.go ./
RUN  go mod init nameThatDoesNotMatter

RUN go build ./import.go

FROM ubuntu:18.04 AS build_stage

RUN \
    apt-get -qq update && \
    apt-get -qq install -y \
	cmake \
        curl \
        g++ \
        git \
        libboost-dev \
        libboost-filesystem-dev \
        libboost-system-dev \
        libbz2-dev \
        libexpat1-dev \
        liblua5.2-dev \
        libpq-dev \
        libproj-dev \
        lua5.2 \
        make \
        python \
        zlib1g-dev

# Building osm2pgsql from source
WORKDIR /
RUN git clone git://github.com/openstreetmap/osm2pgsql.git
WORKDIR /osm2pgsql/build
RUN cmake .. && make -j $(nproc) && make -j $(nproc) install;

FROM ubuntu:18.04 
RUN \
    apt-get -qq update && \
    apt-get -qq install -y \
        curl \
        libexpat1-dev \
        libpq-dev \
        liblua5.2-dev \
        libproj-dev 

COPY --from=build_stage /usr/local/bin/osm2pgsql /usr/local/bin/osm2pgsql
ADD https://raw.githubusercontent.com/gravitystorm/openstreetmap-carto/master/openstreetmap-carto.lua /carto/openstreetmap-carto.lua
ADD https://raw.githubusercontent.com/gravitystorm/openstreetmap-carto/master/openstreetmap-carto.style /carto/openstreetmap-carto.style

COPY ./mapping.yml /mapping.yml
COPY ./scripts/ /scripts/
COPY --from=script_stage /import /import

ENTRYPOINT [ "/import" ]
CMD []
