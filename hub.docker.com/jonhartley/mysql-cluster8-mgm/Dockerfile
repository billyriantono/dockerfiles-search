FROM centos:latest

RUN yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm; \
yum-config-manager --enable mysql-cluster-8.0-community; \
yum -y install epel-release; \
yum -y upgrade; \
groupadd -g 27 mysql; \
useradd -g mysql -m -u 27 -s /bin/bash -d /var/lib/mysqlcluster mysql; \
yum -y install mysql-cluster-community-management-server mysql-cluster-community-ndbclient mysql-cluster-community-client psmisc nc iperf which pv e2fsprogs; \
yum clean all; \
rm -rf /var/cache/yum

COPY entrypoint.sh /entrypoint.sh

EXPOSE 1186
ENTRYPOINT ["/entrypoint.sh"]




