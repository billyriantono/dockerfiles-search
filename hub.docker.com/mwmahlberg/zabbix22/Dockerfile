FROM ubuntu:14.04
MAINTAINER Markus W Mahlberg "markus.mahlberg@me.com"
RUN apt-get update && DEBIAN_FRONTEND="noninteractive" apt-get -y install zabbix-server-mysql zabbix-agent php5-mysql zabbix-frontend-php  openssh-server openssh-client supervisor
RUN service mysql start && echo "CREATE DATABASE zabbix; GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';FLUSH PRIVILEGES" | mysql && service mysql stop
RUN service mysql start && zcat /usr/share/zabbix-server-mysql/schema.sql.gz /usr/share/zabbix-server-mysql/images.sql.gz /usr/share/zabbix-server-mysql/data.sql.gz | mysql zabbix && service mysql stop
RUN sed -i 's:^#.*DBSocket=.*:DBSocket=/var/run/mysqld/mysqld.sock:' /etc/zabbix/zabbix_server.conf && sed -i 's/START=no/START=yes/' /etc/default/zabbix-server
RUN cp /usr/share/doc/zabbix-frontend-php/examples/apache.conf /etc/apache2/conf-available/zabbix-frontend-php.conf && ln -s /etc/apache2/conf-available/zabbix-frontend-php.conf /etc/apache2/conf-enabled/zabbix-frontend-php.conf
RUN sed  -i -e 's/^post_max_size =.*/post_max_size = 16M/' -e 's/^max_execution_time.*/max_execution_time = 300/' -e 's/^max_input_time.*/max_input_time = 300/' -e 's/;date.timezone.*/date.timezone = UTC/' /etc/php5/apache2/php.ini
COPY etc/zabbix/zabbix.conf.php /etc/zabbix/zabbix.conf.php
COPY etc/supervisor/ /etc/supervisor
RUN install -d -o zabbix -g zabbix -m 0755 /var/run/zabbix/
EXPOSE 80 22
CMD /usr/bin/supervisord -n -c /etc/supervisor/supervisord.conf 
