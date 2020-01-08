## Variables
ARG MARIADB_VERSION=latest
ARG MARIADB_DATABASE=mariadb

## Base image
FROM mariadb:${MARIADB_VERSION}

## Mariadb configuration
COPY mariadb.cnf /etc/mysql/conf.d/

## Initialization
COPY db.sql /docker-entrypoint-initdb.d/
