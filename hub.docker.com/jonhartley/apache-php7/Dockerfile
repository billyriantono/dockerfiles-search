FROM jonhartley/c7-systemd

COPY configcreate.service /etc/systemd/system/configcreate.service
COPY configcreate.sh /configcreate.sh

RUN yum -y upgrade; \
yum -y install epel-release; \
yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm; \
yum -y install deltarpm yum-utils; \
yum -y install https://dl.influxdata.com/telegraf/releases/telegraf-1.5.2-1.x86_64.rpm; \
yum-config-manager --enable remi-php72; \
yum -y install http://rpmfind.net/linux/epel/7/x86_64/Packages/p/php-channel-nrk-1.3-1.el7.noarch.rpm; \
yum -y install php php-opcache php-pecl-mcrypt php-pecl-amqp php-cli php-pecl-redis php-gd php-pdo php-curl php-mysqlnd php-ldap php-zip php-fileinfo php-pecl-memcached php-nrk-Predis httpd; \
yum clean all; \
systemctl daemon-reload; \
systemctl enable configcreate.service

EXPOSE 80 9117
ENTRYPOINT ["/usr/sbin/init"]
