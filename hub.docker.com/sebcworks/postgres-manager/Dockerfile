# Dockerfile to install and run a PostgreSQL "manager", that is, a container to manage the postgreSQL database(s).
## BASED PART FROM POSTGRES OFFICIAL REPO
## https://hub.docker.com/_/postgres/

FROM debian:jessie
MAINTAINER Sebastien Collin <sebastien.collin@sebcworks.fr>

# ------------------------------------

# Create the postgres user and group (Thus, we are Ok with other containers uid/gid)
RUN groupadd -r postgres && useradd -r -g postgres postgres

# grab gosu for easy step-down from root
RUN gpg --keyserver pgp.mit.edu --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/* \
    && curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
    && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu \
    && apt-get purge -y --auto-remove curl

# make the "en_US.UTF-8" locale so postgres will be utf-8 enabled by default
RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

RUN apt-key adv --keyserver pgp.mit.edu --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8
ENV PG_MAJOR 9.5

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ wheezy-pgdg main' $PG_MAJOR > /etc/apt/sources.list.d/pgdg.list
RUN apt-get update \
    && apt-get install -y \
       postgresql-client-$PG_MAJOR \
       postgresql-doc-$PG_MAJOR \
    && rm -rf /var/lib/apt/lists/*

#RUN mkdir -p /var/run/postgresql && chown -R postgres /var/run/postgresql

RUN apt-get update && apt-get install -y \
    ftp \
    less \
    nano \
    telnet

# -----------------------------------

# Launching
CMD ["/bin/bash"]
