FROM twdevops/base
MAINTAINER ShawnMa <qsma@thoughtworks.com>

## Add repository
RUN \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ACCC4CF8 &&\
  echo "deb http://apt.postgresql.org/pub/repos/apt trusty-pgdg main" > /etc/apt/sources.list.d/postgres.list

## Update and Install packages
RUN \
  apt-get update &&\
  apt-get install -y --no-install-recommends postgresql-9.4-postgis-2.1 postgresql-contrib-9.4 python-psycopg2 &&\
  rm -rf /var/lib/apt/lists/*

## Install configurations
ADD files/pg_hba.conf     /etc/postgresql/9.4/main/pg_hba.conf
ADD files/postgresql.conf /etc/postgresql/9.4/main/postgresql.conf
ADD files/start.conf      /etc/postgresql/9.4/main/start.conf
RUN \
  mkdir -p /var/run/postgresql && \
  chown -R postgres /var/run/postgresql

## Install scripts
ADD docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod a+x            /docker-entrypoint.sh

ENV PATH   /usr/lib/postgresql/9.4/bin:$PATH
ENV PGDATA /var/lib/postgresql/data

EXPOSE 5432

ENTRYPOINT ["/docker-entrypoint.sh"]

VOLUME ["/var/lib/postgresql/data"]

CMD ["postgres"]


