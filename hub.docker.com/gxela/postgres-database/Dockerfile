FROM ubuntu:12.04

MAINTAINER Alex Goretoy <alex@goretoy.com>

ENV PGDATA_USER postgres
ENV PGDATA_PASS postgres

# Install packages and set language here instead of shell script, so to start after this part during subsequent builds
RUN export DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8 && export LANGUAGE="en_US.UTF-8" && export LANG="en_US.UTF-8" && export LC_ALL="en_US.UTF-8"

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8 && \
    echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/postgresql.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 136221EE520DDFAF0A905689B9316A7BC7917B12 && \
    echo "deb http://ppa.launchpad.net/chris-lea/node.js/ubuntu precise main" > /etc/apt/sources.list.d/nodejs.list && \
    echo "deb-src http://ppa.launchpad.net/chris-lea/node.js/ubuntu precise main" >> /etc/apt/sources.list.d/nodejs.list

RUN apt-get update && \
    apt-get install -y --force-yes \
            g++ \
            make \
            cmake \
            sudo \
            git \
            curl \
            wget \
            gawk \
            build-essential \
            ruby-full \
            rubygems \
            nodejs \
            libboost-all-dev \
            libcurl4-gnutls-dev \
            python-software-properties \
            software-properties-common \
            libpq-dev \
            pgadmin3 \
            postgresql-9.3 \
            postgresql-client-9.3 \
            postgresql-contrib-9.3 \
            postgresql-9.3-plv8 \
            postgresql-9.3-postgis-2.1 \
            postgresql-server-dev-9.3 \
    && apt-get clean && rm -Rf /var/cache/apt


ADD functions/ /functions
ADD extensions/ /extensions
ADD scripts/ /scripts
ADD data/ /data

ADD setup-database.sh /setup-database.sh
RUN /setup-database.sh

EXPOSE 5432

VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

USER postgres

# Set the default command to run when starting the container
CMD ["/usr/lib/postgresql/9.3/bin/postgres", "-D", "/var/lib/postgresql/9.3/main", "-c", "config_file=/etc/postgresql/9.3/main/postgresql.conf"]