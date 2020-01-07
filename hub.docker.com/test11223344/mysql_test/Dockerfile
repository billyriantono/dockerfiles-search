FROM mysql
MAINTAINER testuser
COPY ./my_test.cnf /etc/mysql/conf.d/
COPY init.sh /docker-entrypoint-initdb.d/
RUN echo "test"
