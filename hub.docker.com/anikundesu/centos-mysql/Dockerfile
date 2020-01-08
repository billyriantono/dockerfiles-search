FROM centos:centos6

MAINTAINER Takashi Kanai (@anikundesu)

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mysql && useradd -r -g mysql mysql

# Install Mysql Community Server repository
RUN yum localinstall -y http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm
RUN yum install -y mysql-community-server

ENV MYSQL_MAJOR 5.6
ENV MYSQL_VERSION 5.6.21


WORKDIR /
VOLUME /var/lib/mysql

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld", "--datadir=/var/lib/mysql","--socket=/var/run/mysqld/mysqld.socket", "--user=mysql"]
