# See https://hub.docker.com/r/_/postgres/tags/ for available versions
ARG PG_VERSION=10

# The base image has Postgres pre-installed
FROM postgres:${PG_VERSION}

MAINTAINER Elctriq Power https://electriqpower.com

ENV PG_VERSION ${PG_VERSION:-10}
ENV TIMESCALEDB_VERSION ${TIMESCALEDB_VERSION:-1.0.0}
ENV POSTGIS_VERSION ${POSTGIS_VERSION:-2.4}

### ### ###

### electriqpower1/custom-postgres

# In addition to above, this docker file installs:
# - postgis
# - TimescaleDB
# - PipelineDB
# - pgbundle
# - [[Other extensions specified by Pgfile]]

# e => error out on command error; x => print commands before executing
RUN set -ex

### ### ###

### postgis and postgis scripts

RUN apt-get update -yq \
    && apt-get install -yy postgresql-10-postgis-${POSTGIS_VERSION} postgresql-10-postgis-${POSTGIS_VERSION}-scripts

RUN apt-get install -yy curl wget apt-transport-https apt-utils

### ### ###

### timescaledb

# Instructions: https://docs.timescale.com/v1.0/getting-started/installation/linux/installation-apt-debian
RUN sh -c "echo 'deb https://packagecloud.io/timescale/timescaledb/debian/ `lsb_release -c -s` main' > /etc/apt/sources.list.d/timescaledb.list" \
    && wget --quiet -O - https://packagecloud.io/timescale/timescaledb/gpgkey | apt-key add - \
    && apt-get update -yq

RUN apt-get install -yy timescaledb-postgresql-10

### ### ###

### pipelinedb (debian package)

# Instructions: http://docs.pipelinedb.com/installation.html
ENV PIPELINEDB_VERSION ${PIPELINEDB_VERSION:-1.0.0-6}

RUN mkdir -p /tmp
WORKDIR /tmp
RUN export PG_MAJOR_VERSION=$(echo "${PG_VERSION}" | cut -d'.' -f1-1) \
    && PIPELINEDB_PACKAGE="pipelinedb-postgresql-${PG_MAJOR_VERSION}_${PIPELINEDB_VERSION}.debian9_amd64.deb" \
    && wget https://github.com/pipelinedb/pipelinedb/releases/download/${PIPELINEDB_VERSION}/${PIPELINEDB_PACKAGE} \
    && dpkg -i ${PIPELINEDB_PACKAGE}

### ### ###

### pgbundle

# Install ruby and rubygems for pgbundle
RUN apt-get install -yy ruby ruby-dev gcc build-essential git

# Install pgbundle
RUN gem install pgbundle

### ### ###

### Update postgresql.conf shared_preload_libraries

RUN sed -r -i "s/[#]*\s*(shared_preload_libraries)\s*=\s*'(.*)'/\1 = 'pg_stat_statements,pipelinedb,timescaledb,\2'/;s/,'/'/" \
    /usr/share/postgresql/postgresql.conf.sample \
    && service postgresql restart

### ### ###

### Install pgfile extensions

# Install extension dependencies
RUN apt-get install -yy flex
RUN apt-get install -yy mysql-server
RUN apt-get install -yy mysql-client

# For mysql_fdw
RUN apt-get install -yq libmariadbclient-dev

# Copy Pgfile for installing extensions using pgbundle
RUN mkdir -p /config
COPY config/Pgfile /config/

# Run pgbundle install
WORKDIR /config
RUN $(nohup /docker-entrypoint.sh postgres > /dev/null &) \
    && echo "Waiting for postgres to start..." \
    && sleep 20 \
    && pgbundle install Pgfile

ENTRYPOINT ["/docker-entrypoint.sh", "postgres"]
