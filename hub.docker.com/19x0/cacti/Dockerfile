FROM centos:7

ADD cacti.txt /
ADD entrypoint.sh /
RUN \
    rpm --rebuilddb && yum clean all && \
    yum update -y && \
    yum install -y epel-release && \
    yum install -y httpd php php-mysql php-xml php-snmp php-gd php-mbstring php-ldap php-process &&\
    yum install -y wget patch curl rrdtool net-snmp net-snmp-devel net-snmp-utils mariadb-devel cronie mailx sendmail &&\
    yum remove -y gcc mariadb-devel net-snmp-devel && \
    yum clean all && \
    chmod +x /entrypoint.sh
ADD tz.ini /etc/php.d/

EXPOSE 80
CMD ["sh","/entrypoint.sh"]