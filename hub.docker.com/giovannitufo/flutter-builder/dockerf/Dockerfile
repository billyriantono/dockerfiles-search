FROM ubuntu:14.04
MAINTAINER Giorgos Argyriou <gioargyr@gmail.com>


# INSTALL PREREQUISITIES
RUN apt-get update \
 && apt-get install -y \
    wget \
    default-jdk \
    python-apsw \
    curl \
    git \
    mercurial \
    maven \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# DOWNLOAD AND INSTALL postgres AND postgis
RUN touch /etc/apt/sources.list.d/pgdg.list \
 && echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list.d/pgdg.list \
 && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN apt-get update \
 && apt-get install -y \
    postgresql-9.4 \
    postgresql-server-dev-9.4 \
    postgresql-9.4-postgis-2.3 \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

ADD initdb.sh enable_remote.sh /usr/local/bin/

RUN chmod -v +x /usr/local/bin/initdb.sh
RUN chown -v postgres:postgres /usr/local/bin/initdb.sh
RUN chmod -v +x /usr/local/bin/enable_remote.sh

USER postgres

## start postgres, add postgis, create template for strabon and stop postgres
RUN initdb.sh

USER root

## SOLVING THE MOST STUPID BUG OF ALL TIME:
RUN mkdir /etc/ssl/private-copy \
 && mv /etc/ssl/private/* /etc/ssl/private-copy/ \
 && rm -r /etc/ssl/private \
 && mv /etc/ssl/private-copy /etc/ssl/private \
 && chmod -R 0700 /etc/ssl/private \
 && chown -R postgres /etc/ssl/private

CMD enable_remote.sh && su - postgres -c "/usr/lib/postgresql/9.4/bin/postgres -D /var/lib/postgresql/9.4/main -c config_file=/etc/postgresql/9.4/main/postgresql.conf"