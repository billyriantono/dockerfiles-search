FROM uomresplatdevops/galera-common
MAINTAINER Tim Dettrick <t.dettrick@uq.edu.au>

RUN apt-get install -y mariadb-galera-server-10.0 galera-3

RUN rm /etc/mysql/conf.d/*.cnf

COPY /etc/mysql/conf.d /etc/mysql/conf.d

VOLUME /data

EXPOSE 3306 4444 4567

ENTRYPOINT ["/usr/bin/mysqld_safe"]
