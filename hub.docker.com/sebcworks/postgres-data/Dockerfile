# Dockerfile to "install" and create a data container for PostgreSQL.
# Will kept database and logs data

FROM debian:wheezy
MAINTAINER Sebastien Collin <sebastien.collin@sebcworks.fr>

# ------------------------------------

# Create the postgres user and group before anything else (to ensure uid/gid number consistency across builds)
RUN groupadd -r postgres \
    && useradd -r -g postgres postgres

# Volume creation
RUN mkdir -p /data/postgresql \
    && chown -R postgres:postgres /data/postgresql

VOLUME /data/postgresql
VOLUME /var/log

USER postgres

# -----------------------------------

# "Launching" with something that allow you to know what this container is about
CMD ["echo", "Data container for PostgreSQL"]
