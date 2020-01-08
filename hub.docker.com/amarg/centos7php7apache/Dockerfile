FROM centos/httpd
MAINTAINER AMAR GUPTA <amarthebond@gmail.com>
RUN yum -y update && yum -y install deltarpm && yum install -y epel-release && yum clean all
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
RUN yum install -y php7* --skip-broken && yum clean all
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer