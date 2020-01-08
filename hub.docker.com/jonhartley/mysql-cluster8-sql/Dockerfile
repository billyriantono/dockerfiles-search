FROM centos:latest

RUN yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm; \
yum-config-manager --enable mysql-cluster-8.0-community; \
yum -y install epel-release; \
yum -y install mysql-cluster-community-server mysql-cluster-community-memcached psmisc which; \
yum clean all; \
rm -rf /var/cache/yum

COPY entrypoint.sh /entrypoint.sh

EXPOSE 3306 33060 11211
ENTRYPOINT ["/entrypoint.sh"]




