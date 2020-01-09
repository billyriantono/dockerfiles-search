FROM jonhartley/c7-systemd

COPY configcreate.service /etc/systemd/system/configcreate.service
COPY configcreate.sh /configcreate.sh

RUN yum -y upgrade; \
yum -y install epel-release; \
yum -y install https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm; \
yum -y install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm;\
yum -y install https://lefred.be/wp-content/uploads/2018/09/sysbench-1.0.15-1.el7_.centos.x86_64.rpm; \
yum -y install httpd-tools bind-utils iperf net-tools mysql nc psmisc traceroute postgresql10; \
mkdir -p /scripts; \
yum clean all; \
rm -rf /var/cache/yum; \
systemctl daemon-reload; \
systemctl enable configcreate.service

COPY scripts /scripts

EXPOSE 5432
