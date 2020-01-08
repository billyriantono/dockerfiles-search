FROM yooqe/base

RUN aptitude update -y
RUN aptitude install -y mysql-server

RUN mkdir -p /var/run/mysqld
RUN chown mysql:mysql /var/run/mysqld

ADD entrypoint.sh /entrypoint.sh
ADD my.cnf /etc/mysql/my.cnf

EXPOSE 3306

ENTRYPOINT ["/entrypoint.sh"]
CMD ["mysqld", "--datadir=/data/mysql", "--user=mysql"]
