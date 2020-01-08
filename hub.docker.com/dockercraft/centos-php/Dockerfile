# How-To
 # Local Build: docker build -t php .
 # Local Run: docker run -it --rm php

FROM centos:7.5.1804
MAINTAINER Duan Li <inputx@goodays.com>

# User/Group
ENV MY_USER="www-data" \
	MY_GROUP="www-data" \
	MY_UID="1000" \
	MY_GID="1000"

RUN groupadd -g ${MY_GID} -r ${MY_GROUP} && \
	adduser -u ${MY_UID} -m -s /bin/bash -g ${MY_GROUP} ${MY_USER} && \
	yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y && \
	yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y && \
	yum install unzip git yum-utils -y && \
	yum-config-manager --enable remi-php56 && \
	yum install php php-cli php-fpm php-common php-bcmath php-ldap php-mcrypt php-mbstring php-gd php-opcache php-odbc php-soap php-xml php-xmlrpc php-pgsql php-pdo php-mysqlnd php-pecl-xdebug php-mssql composer.noarch -y && \
	yum clean all && \
	rm -rf /var/cache/yum && \
	composer global require "hirak/prestissimo" -v && \
	composer global require "phpunit/phpunit" "codeception/codeception" -v && \
	composer clearcache
	

ENV PATH="/root/.composer/vendor/bin:${PATH}"

EXPOSE 80 8000 8080 8008 8800 9000 443

