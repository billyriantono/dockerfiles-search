FROM mysql:latest

COPY ./sql-scripts/ /docker-entrypoint-initdb.d/
COPY ./configs/charset.cnf /etc/mysql/conf.d/
COPY ./configs/charset.cnf /etc/mysql/conf.d/