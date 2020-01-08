FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD=root

ADD 100-dump.sql docker-entrypoint-initdb.d/100-dump.sql

