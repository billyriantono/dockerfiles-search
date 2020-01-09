# NAME: MariaDB
#
# DESCRIPTION: MariaDB image.
#
# REQUIRED ENVS: DATA_DIRECTORY
#
# OPTIONAL ENVS: ROOT_PASSWORD
#
# USAGE EXAMPLE: docker run websend/mariadb
# BUILD EXAMPLE: docker build -t websend/mariadb:10.1 .

FROM websend/debian:7.7
MAINTAINER Ilja Krijger <i.krijger@websend.nl>

Add files/mariadb.list /etc/apt/sources.list.d/mariadb.list

RUN \
  apt-key adv --keyserver keys.gnupg.net --recv-keys 0xcbcb082a1bb943db && \
  useradd -m -u 3306 mysql && \
  apt-get update && \
  apt-get install -yq mariadb-server && \
  apt-get install -yq inotify-tools && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
  rm -rf /etc/mysql/conf.d/mysqld_safe_syslog.conf

ADD files/my.cnf /etc/mysql/my.cnf
ADD files/scripts /usr/local/bin

RUN \
  chmod 0640 /etc/mysql/my.cnf && \
  chmod +x /usr/local/bin/run.sh && \
  chown -R mysql:mysql /etc/mysql/

ENV TERM dumb

EXPOSE 3306

USER mysql

ENTRYPOINT ["/bin/bash", "/usr/local/bin/run.sh"]
