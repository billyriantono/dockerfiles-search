FROM phusion/baseimage:0.9.15
MAINTAINER Ben Firshman <ben@orchardup.com>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -qq && apt-get install -y mysql-server-5.5

ADD my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 664 /etc/mysql/conf.d/my.cnf
ADD run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

ADD mysql_create_db /usr/local/bin/mysql_create_db
RUN chmod +x /usr/local/bin/mysql_create_db

ADD mysqldump_with_env /usr/local/bin/mysqldump_with_env
RUN chmod +x /usr/local/bin/mysqldump_with_env

ADD mysql_with_env /usr/local/bin/mysql_with_env
RUN chmod +x /usr/local/bin/mysql_with_env

VOLUME ["/var/lib/mysql"]
EXPOSE 3306
CMD ["/usr/local/bin/run"]
