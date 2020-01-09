FROM mysql:5.7.9


ENV MYSQL_ROOT_PASSWORD root
ENV MYSQL_DATABASE batmeca

COPY batmeca.sql /docker-entrypoint-initdb.d/

EXPOSE 3306