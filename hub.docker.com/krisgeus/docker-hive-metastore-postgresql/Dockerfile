FROM postgres:9.5.3

MAINTAINER "Ivan Ermilov <ivan.s.ermilov@gmail.com>"

ADD hive-schema-3.1.0.postgres.sql /hive/hive-schema-3.1.0.postgres.sql

ADD init-hive-db.sh /docker-entrypoint-initdb.d/init-user-db.sh
