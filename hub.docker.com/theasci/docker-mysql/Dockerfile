FROM centos:centos6
MAINTAINER Mason Malone <masonm@the-jci.org>

RUN yum -y upgrade
RUN yum install -y http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm
RUN yum install -y mysql-community-server

RUN rm /etc/my.cnf && mkdir -p /etc/mysql/conf.d
ADD my.cnf /etc/mysql/my.cnf
RUN chmod 664 /etc/mysql/my.cnf
ADD setup_mysql.sh /usr/local/bin/setup_mysql.sh
RUN chmod +x /usr/local/bin/setup_mysql.sh
RUN "/usr/local/bin/setup_mysql.sh"

CMD ["/usr/sbin/mysqld", "--skip-name-resolve", "--skip-host-cache"]
