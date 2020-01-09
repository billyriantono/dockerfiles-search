FROM hsihung/c7-systemd
RUN yum -y install net-tools lrzsz wget unzip telnet gcc make gd gd-devel net-snmp epel-release; \
yum -y install java httpd php php-gd php-mbstring php-mysqlnd php-soap php-pecl-memcache memcached freetds; \
yum -y install php-pear php-devel php-mssql httpd-devel pcre-devel php-odbc; \
yum clean all; \
printf "\n" | pecl install apc; \
pecl install xdebug; \
useradd -m -p !QAZ2wsx web; \
usermod -a -G apache web; \
systemctl enable httpd.service;
COPY 38dee.conf /etc/httpd/conf.d/
COPY apc.ini /etc/php.d/
COPY 38dee.ini /etc/php.d/
COPY xdebug.ini /etc/php.d/
COPY odbc.ini /etc/
VOLUME /etc/php.d
EXPOSE 80
CMD ["/usr/sbin/init"]
