FROM debian:latest

# vars
ENV DEBIAN_FRONTEND noninteractive
ENV OSM_VERSION 3.1.0
ENV PHP_VERSION 7.0
ENV POSTGIS_VERSION 2.4
ENV POSTGRESQL_VERSION 10
ENV POSTGRESQL_SHARED_BUFFERS 2GB
ENV POSTGRESQL_MAINTENANCE_WORK_MEM 10GB
ENV POSTGRESQL_WORK_MEM 50MB
ENV POSTGRESQL_EFFECTIVE_CACHE_SIZE 24GB
ENV POSTGRESQL_SYNCHRONOUS_COMMIT off
ENV POSTGRESQL_CHECKPOINT_TIMEOUT 10min
ENV POSTGRESQL_CHECKPOINT_COMPLETION_TARGET 0.9
ENV POSTGRESQL_MAX_CONNECTIONS 150

# install base depdendencies
RUN apt-get update -qq && apt-get upgrade -y
RUN apt-get install -y locales apt-utils tzdata wget lsb-release gnupg2

# setup os
RUN echo "ru_RU.UTF-8 UTF-8" > /etc/locale.gen && locale-gen ru_RU.UTF-8 && update-locale LANG=ru_RU.UTF-8
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata

ENV LANGUAGE ru_RU.UTF-8
ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8
ENV TZ Europe/Moscow

# setup repositories
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'


# install nominatim dependencies
RUN apt-get update -qq && apt-get upgrade -y
RUN apt-get install -y build-essential cmake g++ libboost-dev libboost-system-dev \
                        libboost-filesystem-dev libexpat1-dev zlib1g-dev libxml2-dev\
                        libbz2-dev libpq-dev libproj-dev \
                        postgresql-server-dev-$POSTGRESQL_VERSION postgresql-$POSTGRESQL_VERSION-postgis-$POSTGIS_VERSION \
                        apache2 php$PHP_VERSION php$PHP_VERSION-pgsql libapache2-mod-php php-pear php-db \
                        php$PHP_VERSION-intl


# setup users
RUN useradd -d /srv/nominatim -s /bin/bash -m nominatim

# setup nominatim
USER nominatim

WORKDIR /srv/nominatim
RUN mkdir /srv/nominatim/importdata
RUN wget https://nominatim.org/release/Nominatim-$OSM_VERSION.tar.bz2
RUN tar xf Nominatim-$OSM_VERSION.tar.bz2 && mv Nominatim-$OSM_VERSION src
RUN ls /srv/nominatim/ && ls /srv/nominatim/src
RUN wget -O /srv/nominatim/src/data/country_osm_grid.sql.gz https://www.nominatim.org/data/country_grid.sql.gz

WORKDIR /srv/nominatim/src
RUN mkdir build && cd build && cmake .. && make
COPY configs/nominatim-local.php /srv/nominatim/src/build/settings/local.php

# swap user
USER root

# setup postgresql
RUN service postgresql start && \
    su - postgres -c "createuser -s nominatim" && \
    su - postgres -c "createuser -s www-data" && \
    service postgresql stop


# setup apache
COPY configs/apache2-nominatim.conf /etc/apache2/sites-enabled/000-default.conf

# copy files
COPY entrypoint.sh /srv/scripts/
COPY scripts/* /srv/scripts/

#ENV OSM_DATA http://download.geofabrik.de/russia-latest.osm.pbf
ENV OSM_DATA http://download.geofabrik.de/russia/crimean-fed-district-latest.osm.pbf
RUN /srv/scripts/import-osm-data.sh

EXPOSE 80
CMD /srv/scripts/entrypoint.sh
