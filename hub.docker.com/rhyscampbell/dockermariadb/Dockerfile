FROM centos:8
LABEL maintainer="github.com/rhysmeister"
RUN yum update -y

COPY resources/mariadb.repo /etc/yum.repos.d/
COPY resources/default.cnf  /etc/my.cnf.d/

RUN yum clean all
RUN yum install boost-program-options -y && yum install  --enablerepo=mariadb --disablerepo=AppStream MariaDB-server -y

EXPOSE 3306/tcp

USER mysql
COPY resources/mariadb.sql /var/run/mysql/
CMD ["mysqld"]
