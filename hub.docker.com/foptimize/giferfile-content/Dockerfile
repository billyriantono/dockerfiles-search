FROM postgres:9.3

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get -qfy install postgis postgresql-9.3-postgis-2.1 \
  && apt-get clean
