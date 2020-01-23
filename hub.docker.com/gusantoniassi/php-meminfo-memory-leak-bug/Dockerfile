FROM centos:6.9

RUN yum install -y \
	git \
	gcc \
	gcc-c++ \
	autoconf \
	automake \
	https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm \
	http://rpms.remirepo.net/enterprise/remi-release-6.rpm \
	yum-utils
	
RUN yum-config-manager --enable remi-php71 && \
	yum install -y \
		php \
		php-cli \
		php-devel \
		php-pear
		
RUN git clone https://github.com/BitOne/php-meminfo.git /opt/php-meminfo
WORKDIR /opt/php-meminfo/extension/php7
RUN phpize && \
	./configure --enable-meminfo && \
	make && \
	make install

WORKDIR /
