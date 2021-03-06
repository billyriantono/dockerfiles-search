# NAME: PostgreSQL Upgrade.
#
# DESCRIPTION: PostgreSQL Upgrade image.
#
# REQUIRED ENVS:
# DATA_DIRECTORY (ie. "/home/postgresql/data/")
#
# OPTIONAL ENVS:
#
# OTHER:
# Process to migrate data between PostgreSQL versions:
# 1. Turn off old PostgreSQL container.
# 2. docker run --rm --volumes-from postgresql_master_data -v $(pwd):/backup thedutchselection/debian:8.7 tar cvf /backup/backup.tar /home/postgres/data/
# 3. docker run -e DATA_DIRECTORY=/home/postgres/data --volumes-from postgresql_master_data --rm thedutchselection/postgresql_upgrade:9.4_9.6
#
# The data container should now be migrated and ready for the new PostgreSQL container. If something goes wrong, recover
# the old data container by the following commands:
# 1. docker rm postgresql_master_data
# 2. docker run --name postgresql_master_data -e "DATA_DIRECTORY=/home/postgres/data/" -e "USER_ID=5432" -e "GROUP_ID=5432" -v /home/postgres/data/ thedutchselection/data:latest
# 3. docker run --volumes-from postgresql_master_data -v $(pwd):/backup thedutchselection/debian:8.7 tar xvf /backup/backup.tar

FROM thedutchselection/debian:8.7
MAINTAINER Gerard Meijer <g.meijer@thedutchselection.com>

RUN \
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
  echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
  apt-get update && \
  apt-get install -yq python-software-properties && \
  apt-get install -yq software-properties-common && \
  useradd -m -u 5432 postgres && \
  apt-get install -yq postgresql-9.4=9.4.11-1.pgdg80+1 && \
  apt-get install -yq postgresql-client-9.4=9.4.11-1.pgdg80+1 && \
  apt-get install -yq postgresql-contrib-9.4=9.4.11-1.pgdg80+1 && \
  apt-get install -yq postgresql-server-dev-9.4=9.4.11-1.pgdg80+1 && \
  apt-get install -yq postgresql-9.6=9.6.2-1.pgdg80+1 && \
  apt-get install -yq postgresql-client-9.6=9.6.2-1.pgdg80+1 && \
  apt-get install -yq postgresql-contrib-9.6=9.6.2-1.pgdg80+1 && \
  apt-get install -yq postgresql-server-dev-9.6=9.6.2-1.pgdg80+1 && \
  apt-get install -yq inotify-tools && \
  apt-get install -yq psmisc && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD files/pg_hba.conf /etc/postgresql/9.4/main/
ADD files/pg_ident.conf /etc/postgresql/9.4/main/
ADD files/postgresql_9_4_template.conf /etc/postgresql/9.4/main/
ADD files/pg_hba.conf /etc/postgresql/9.6/main/
ADD files/pg_ident.conf /etc/postgresql/9.6/main/
ADD files/postgresql_9_6_template.conf /etc/postgresql/9.6/main/
ADD files/scripts /usr/local/bin

RUN \
  chmod 640 /etc/postgresql/9.4/main/pg_hba.conf && \
  chmod 640 /etc/postgresql/9.4/main/pg_ident.conf && \
  chmod 644 /etc/postgresql/9.4/main/postgresql_9_4_template.conf && \
  chmod 640 /etc/postgresql/9.6/main/pg_hba.conf && \
  chmod 640 /etc/postgresql/9.6/main/pg_ident.conf && \
  chmod 644 /etc/postgresql/9.6/main/postgresql_9_6_template.conf && \
  chmod +x /usr/local/bin/run.sh && \
  chown -R postgres:postgres /etc/postgresql/9.4/main && \
  chown -R postgres:postgres /etc/postgresql/9.6/main && \
  chown postgres:postgres /usr/local/bin/*

EXPOSE 5432

USER postgres

ENTRYPOINT ["/bin/bash", "/usr/local/bin/run.sh"]
