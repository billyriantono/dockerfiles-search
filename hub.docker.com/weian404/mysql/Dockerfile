FROM weian404/centos:7.2.1511-systemd
RUN rpm -ivh http://repo.mysql.com//mysql57-community-release-el7-9.noarch.rpm
RUN yum -y install mysql-community-server.x86_64
RUN systemctl enable mysqld.service
