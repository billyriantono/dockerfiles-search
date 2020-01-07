FROM postgres:10.3

MAINTAINER Terry Zhang

RUN apt-get update && apt-get install -y postgresql-contrib

ADD createExtension.sh /docker-entrypoint-initdb.d/
RUN chmod 755 /docker-entrypoint-initdb.d/createExtension.sh
ADD postgresql.conf /var/lib/postgresql/data/postgresql.conf
