FROM mysql:5.6.38
MAINTAINER Denis Arosquipa <darosquipa@dtransforma.com>

COPY ./my.cnf /etc/mysql/conf.d
COPY ./data/*.* /docker-entrypoint-initdb.d

EXPOSE 3306
CMD ["mysqld"]

