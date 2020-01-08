from centos:7

MAINTAINER Mattias Hemmingsson



LABEL name="MaxScale Server"
LABEL vendor="life and shell"

RUN echo -e "[mariadb] \nname = MariaDB \nbaseurl = http://yum.mariadb.org/10.1/centos7-amd64 \ngpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB \ngpgcheck=1 \n "  >  /etc/yum.repos.d/MariaDB.repo

RUN yum install MariaDB-server MariaDB-devel -y
RUN yum -y install make gcc gcc-c++ ncurses-devel bison glibc-devel openssl-devel libaio libaio-devel telnet



#Install maxscale
RUN rpm -i http://downloads.mariadb.com/enterprise/64mr-1jgt/generate/10.1/mariadb-enterprise-repository.rpm
ADD config/maxscale.cnf /etc/maxscale.cnf
RUN yum install maxscale -y


CMD sleep 30 && maxscale -d