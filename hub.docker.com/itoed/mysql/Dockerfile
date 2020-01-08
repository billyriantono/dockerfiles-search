FROM itoed/centos
MAINTAINER Eduardo Ito <itoed@yahoo.com>

# MySQL Community Repository
RUN yum install -y http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm; \
    yum clean all
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

# Yum packages
RUN yum install -y mysql-community-server; yum clean all

# Initialize MySQL
RUN mysql_install_db && chown -R mysql:mysql /var/lib/mysql
