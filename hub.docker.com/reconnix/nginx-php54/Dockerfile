### Dockerfile

FROM reconnix/base:latest
MAINTAINER Russ McKendrick <russ.mckendrick@reconnix.com>

ADD nginx.repo /etc/yum.repos.d/
RUN yum -y install nginx mariadb php php-fpm php-mysql php-pdo php-devel php-gd php-pecl-memcache php-pspell php-snmp php-xmlrpc php-xml php-mcrypt php-mbstring php-imap php-pecl-mailparse php-pecl-xdebug php-pecl-xhprof python-setuptools postfix && yum clean all
RUN easy_install pip && pip install "pip>=1.4,<1.5" --upgrade && pip install supervisor
RUN useradd webserver -u 666 && gpasswd -a webserver apache
ADD conf-supervisord.conf /etc/supervisord.conf
ADD default.conf /etc/nginx/conf.d/default.conf
ADD nginx.conf /etc/nginx/nginx.conf
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
ADD run /usr/local/bin/
RUN chmod +x /usr/local/bin/run
CMD ["/usr/local/bin/run"]