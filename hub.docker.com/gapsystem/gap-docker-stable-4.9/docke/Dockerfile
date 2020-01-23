FROM postgres:9.4.13
ENV POSTGRES_DB my_database
ENV HOSTNAME mypgdb
COPY sql.sql /docker-entrypoint-initdb.d/
