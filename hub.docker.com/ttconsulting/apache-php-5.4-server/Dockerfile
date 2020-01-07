FROM centos:latest

ADD https://codeload.github.com/gnif/mod_rpaf/zip/stable /root/src/rpaf

RUN yum install -y  --nogpgcheck --disableplugin=fastestmirror epel-release
RUN yum install -y  --nogpgcheck --disableplugin=fastestmirror \ 
		php php-devel php-bcmath php-dba php-enchant php-gd \
		php-intl php-ldap php-mbstring php-mysql php-odbc \
		php-pdo php-pgsql php-soap php-xml php-xmlrpc php-pear \
		php-mcrypt make libtool unzip httpd-devel zlib-devel \
		ImageMagick-devel libmemcached-devel msmtp tzdate

RUN pecl install apc memcache memcached imagick	timezonedb

RUN unzip /root/src/rpaf -d /root/src
WORKDIR /root/src/mod_rpaf-stable
RUN make && make install
RUN libtool --finish /usr/lib64/httpd/modules

RUN rm -rf /root/src /etc/timezone
WORKDIR /var/www

EXPOSE 80 443

VOLUME ['/etc/php.d', '/etc/httpd/conf', '/var/www']

ADD run.sh /root/run.sh
RUN chmod +x /root/run.sh
ENTRYPOINT ["/root/run.sh"]
