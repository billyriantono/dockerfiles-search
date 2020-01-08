FROM avkosme/centos

RUN yum -y localinstall https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
RUN yum -y install mysql-community-server

ADD assets/my.cnf.sh /opt/my.cnf.sh
RUN /bin/bash -c 'chmod +x /opt/my.cnf.sh'
RUN /opt/./my.cnf.sh

RUN systemctl enable mysqld.service