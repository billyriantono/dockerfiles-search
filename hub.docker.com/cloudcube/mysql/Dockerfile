FROM cloudcube/base

MAINTAINER DavidZhao <zhaohaibin@outlook.com>

ENV REFRESHED_AT 2015-07-08 18:41

RUN apt-get update \
  && apt-get install -y mysql-server-5.6 \
  && rm -rf /var/lib/mysql/mysql \
  && rm -rf /var/lib/apt/lits/*

ADD assets/mysql_start /assets/mysql_start
ADD config/mysqld.conf /etc/supervisor/conf.d/mysqld.conf

RUN chmod 755 /assets/mysql_start

EXPOSE 3306

VOLUME ["/var/lib/mysql"]
VOLUME ["/run/mysqld"]

CMD ["/assets/mysql_start"]
