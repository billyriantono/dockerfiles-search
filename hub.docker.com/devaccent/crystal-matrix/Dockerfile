FROM centos:latest

MAINTAINER "Alexandru Berce" <alex@devaccent.com>

ENV container docker

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
 && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

RUN yum -y update

# php && httpd
RUN yum -y install php72w php72w-opcache php72w-cli php72w-common php72w-gd php72w-intl php72w-mbstring php72w-mcrypt php72w-mysql php72w-mssql php72w-pdo php72w-pear php72w-soap php72w-xml php72w-xmlrpc php72w-pecl-redis httpd

# Tools
RUN yum -y install epel-release iproute at curl crontabs git

# Pagespeed
RUN curl -O https://dl-ssl.google.com/dl/linux/direct/mod-pagespeed-stable_current_x86_64.rpm \
 && rpm -U mod-pagespeed-*.rpm \
 && yum clean all

# Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php composer-setup.php --install-dir=bin --filename=composer \
 && php -r "unlink('composer-setup.php');"

# Local time
RUN rm -rf /etc/localtime \
 && ln -s /usr/share/zoneinfo/Europe/Bucharest /etc/localtime

# we want some config changes
COPY config/php_settings.ini /etc/php.d/
COPY config/v-host.conf /etc/httpd/conf.d/

# create webserver-default directory
RUN mkdir -p /var/www/app

EXPOSE 80
EXPOSE 443
EXPOSE 9000

RUN systemctl enable httpd \
 && systemctl enable crond

CMD ["/usr/sbin/init"]

ADD config/run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]