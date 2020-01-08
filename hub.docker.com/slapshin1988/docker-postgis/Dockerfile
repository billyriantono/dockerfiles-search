FROM postgres:10

RUN apt-get update -y
RUN apt-get install -y postgresql-10-postgis-2.4

RUN mkdir -p /docker-entrypoint-initdb.d
COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY ./update-postgis.sh /usr/local/bin

