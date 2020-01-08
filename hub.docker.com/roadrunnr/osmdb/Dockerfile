# based on Docker PostrreSQL sample at https://docs.docker.com/engine/examples/postgresql_service

FROM ubuntu:zesty

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update -qq
RUN apt-get install -y -qq --no-install-recommends curl ca-certificates \
            postgresql-9.6-postgis-2.3 postgresql-9.6-postgis-2.3-scripts \
            postgresql-contrib-9.6 osm2pgsql

USER postgres

RUN /etc/init.d/postgresql start && \
    psql --command "CREATE USER gis WITH PASSWORD 'gis';" && \
    createdb -E UTF8 -O gis gis && \
    psql -c "CREATE EXTENSION postgis;" -d gis && \
    psql -c "CREATE EXTENSION hstore;" -d gis

RUN cd /tmp && \
    curl -O https://planet.openstreetmap.org/pbf/planet-latest.osm.pbf && \
    osm2pgsql -d gis -k -s planet-latest.osm.pbf && \
    rm -f planet-latest.osm.pbf

# Adjust PostgreSQL configuration so that remote connections to the
# database are possible.
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.6/main/pg_hba.conf

# And add ``listen_addresses`` to ``/etc/postgresql/9.6/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.6/main/postgresql.conf

# Expose the PostgreSQL port
EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# Set the default command to run when starting the container
CMD ["/usr/lib/postgresql/9.6/bin/postgres", "-D", "/var/lib/postgresql/9.6/main", "-c", "config_file=/etc/postgresql/9.6/main/postgresql.conf"]