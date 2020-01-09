FROM mariadb:10.1.14

COPY ./my.cnf /etc/mysql/
RUN mkdir -p /data/les/mariadb
RUN mkdir /data/les/tolocus
RUN mkdir -p /data/les/fromlocus/processed
RUN echo "create database les;" > /docker-entrypoint-initdb.d/create_database.sql
RUN echo "create user les identified by 'les';grant all on les.* to les;" > /docker-entrypoint-initdb.d/create_user.sql
