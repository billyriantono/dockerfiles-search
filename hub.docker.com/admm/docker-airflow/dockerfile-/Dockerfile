FROM mysql:5.7

LABEL maintainer="Debezium Community"

COPY mysql.cnf /etc/mysql/conf.d/
COPY inventory.sql /docker-entrypoint-initdb.d/
COPY account.sql /docker-entrypoint-initdb.d/
COPY my2.sql /docker-entrypoint-initdb.d/