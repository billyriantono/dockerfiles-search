FROM centos:7
MAINTAINER "Mattias Hemmingsson" <matte.hemmingsson@gmail.com>


RUN yum install mariadb-server -y

ADD sql-init.sql /opt/
ADD my.cnf /etc/my.cnf
ADD run.sh /opt/
RUN chmod +x /opt/run.sh
CMD /opt/run.sh
