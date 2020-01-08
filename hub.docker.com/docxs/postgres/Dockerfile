########################################################################
# Dockerfile for Postgres
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Component:    Postgres
# Version:      9.3
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/docxs/docker-postgres
# License:      MIT
########################################################################

# Pull base image
FROM \
  docxs/base:latest

# Maintainer details
MAINTAINER \
  pjan vandaele "pjan@pjan.io"

# Set the environment variables
ENV POSTGRES_VERSION 9.3

# Add the configuration files
ADD config /src/config

# Install postgress
RUN apt-prepare \
 && apt-get install -q -y \
      curl \
 && curl -jksSL http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | apt-key add - \
 && echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list \
 && apt-get update -q -y \
 && apt-get install -q -y \
      pwgen \
      postgresql-9.3 \
      postgresql-contrib-9.3 \
      libgeos-c1 \
      postgresql-9.3-postgis-2.1 \
      libpq-dev \
 && echo "Configuring postgres ..." \
 && pg_dropcluster --stop 9.3 main \
 && cp -f /src/config/etc_postgresql_9.3_main_pg_hba.conf /etc/postgresql/9.3/main/pg_hba.conf \
 && cp -f /src/config/etc_postgresql_9.3_main_pg_ident.conf /etc/postgresql/9.3/main/pg_ident.conf \
 && cp -f /src/config/etc_postgresql_9.3_main_postgresql.conf /etc/postgresql/9.3/main/postgresql.conf \
 && mkdir -p /etc/postgresql/9.3/main/conf.d \
 && chown -R postgres:postgres /etc/postgresql/9.3/main/* \
 && apt-get remove -q -y --purge \
      libpq-dev \
 && apt-cleanup

# Add the binary files
ADD bin /bin/

# Expose the data volume
VOLUME \
  ["/etc/postgresql"]

# Expose the relevant ports
EXPOSE \
  5432

# Run bootstrap on container launch
ENTRYPOINT \
  ["bootstrap"]

# Default command runs the postgres server
CMD \
  ["-server"]

# docker build [--rm] -t <user>/postgres:9.3 .
# docker run -v /data/log -v /data/main --name postgres-data busybox:ubuntu-14.04
# docker run  -d --volumes-from postgres-data -v -p 5432:5432 <user>/postgres:9.3
