FROM postgres:9.4-alpine
MAINTAINER ulisesrcolina [at] gmail [dot] com
ADD 0_esquema.sql /docker-entrypoint-initdb.d
ADD 1_backup.sql /docker-entrypoint-initdb.d
