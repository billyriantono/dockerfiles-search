FROM mysql:8

MAINTAINER Achim Rosenhagen <a.rosenhagen@ffuenf.de>

RUN apt-get update \
  && apt-get install --no-install-recommends -y \
     vim \
     netcat-openbsd

ADD dev.cnf /etc/mysql/conf.d/dev.cnf
ADD remote-access.cnf /etc/mysql/conf.d/remote-access.cnf
ADD performance-schema.cnf /etc/mysql/conf.d/performance-schema.cnf

COPY grant.sql /docker-entrypoint-initdb.d/grant.sql
