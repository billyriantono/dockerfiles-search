FROM weian404/centos:7.2.1511-systemd

RUN rpm -ivh http://repo.zabbix.com/zabbix/3.2/rhel/7/x86_64/zabbix-release-3.2-1.el7.noarch.rpm
RUN yum -y install zabbix-server-mysql zabbix-web-mysql
RUN yum clean all
RUN systemctl enable zabbix-server.service
RUN systemctl enable httpd.service
