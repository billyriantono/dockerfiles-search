# Which base image to use
FROM debian:jessie

# Who is in charge of maintaining this image
MAINTAINER Nathan Jacobson <njacobson@fanforce.com>

# Setup environment variables
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

# Install system packages
RUN apt-get update && apt-get install -y \
    postgresql-9.4 \
    postgresql-client-9.4 \
    postgresql-contrib-9.4 \
    python-software-properties \
    software-properties-common
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Run the rest of the commands as the ``postgres`` user created by
# the ``postgres-9.4`` package when it was ``apt-get installed``
USER postgres

# Adjust PostgreSQL configuration so that remote connections to the database are possible.
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.4/main/pg_hba.conf

# Adjust PostgreSQL configuration so that it listens on all available interfaces
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/main/postgresql.conf
