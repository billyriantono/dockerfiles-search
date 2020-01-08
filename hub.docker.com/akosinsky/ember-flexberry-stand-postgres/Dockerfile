FROM flexberry/alt.p8-postgresql

COPY . /docker/

ARG TAG=1.0.0-beta01-postgresql
RUN cd /docker/host/ ; \ 
  wget https://raw.githubusercontent.com/akosinsky/FlexberryEmberTestStand.ODataBackend/$TAG/SQL/PostgreSql.create.sql  ; \
  /bin/sh /docker/host/createdb.sh

MAINTAINER mail@flexberry.net
