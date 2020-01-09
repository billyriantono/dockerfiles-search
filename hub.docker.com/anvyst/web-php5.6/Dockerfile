FROM centos

# Installing yum utils & setting repository for remi-php56
RUN yum install -y \
	epel-release \
	yum-utils

RUN yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm

# Enabling remi to use PHP56
RUN yum-config-manager --enable remi-php56

# Installing required PHP packages
RUN yum install -y --setopt=tsflags=nodocs \
	php \
	php-mcrypt \
	php-cli \
	php-gd \
	php-curl \
	php-mysql \
	php-ldap \
	php-zip \
	php-fileinfo \
	php-intl \
	php-mbstring \ 
	php-xml \
	php-soap \
	php-opcache

# Installation of other required deps for working with code
RUN yum install -y --setopt=tsflags=nodocs \
	git \
	nginx \
	mariadb \
	net-tools \
	which \
	vim \
	nano \
	zip \
	unzip \

# Clean cache of yum 
RUN yum clean all && \
	rm -rf /var/cache/yum

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

CMD ["/bin/bash"]
