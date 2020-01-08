FROM mysql/mysql-server:5.5
MAINTAINER panage

ENV MYSQL_ALLOW_EMPTY_PASSWORD=yes
ENV MYSQL_ROOT_HOST=172.17.0.1

COPY resources/my.cnf /etc/my.cnf

CMD ["mysqld"]
