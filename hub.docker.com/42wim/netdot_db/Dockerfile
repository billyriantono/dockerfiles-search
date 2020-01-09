FROM blalor/centos
MAINTAINER @42wim

RUN yum install -y mysql-server
RUN /etc/init.d/mysqld start && echo "GRANT ALL ON *.* TO admin@'%' IDENTIFIED BY 'mysql-server' WITH GRANT OPTION; FLUSH PRIVILEGES" | mysql

EXPOSE 3306

CMD /usr/bin/mysqld_safe --datadir=/var/lib/mysql --socket=/var/lib/mysql/mysql.sock --pid-file=/var/run/mysqld/mysqld.pid --basedir=/usr --user=mysql

