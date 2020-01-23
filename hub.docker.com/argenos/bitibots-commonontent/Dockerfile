# Derived from official mysql image (our base image)
FROM mysql

#setting the envirement
ENV MYSQL_ROOT_PASSWORD=12345

EXPOSE 3306

# creating the database user and the data base
COPY ./ElectionManagerDb.sql /docker-entrypoint-initdb.d/
