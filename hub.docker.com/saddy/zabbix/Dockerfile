FROM berngp/docker-zabbix
MAINTAINER Settawut itopplus
#Install packages
RUN yum update -y
Run yum upgrade -y
RUN yum install ssmtp -y

COPY zabbix-sendmail.sh /usr/lib/zabbix/alertscripts/zabbix-sendmail.sh
RUN chmod 755 /usr/lib/zabbix/alertscripts/zabbix-sendmail.sh
