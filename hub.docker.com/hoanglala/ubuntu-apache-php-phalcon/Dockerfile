FROM hoanglala/ubuntu-apache-php

MAINTAINER Hoang Nguyen <nbhoangit@gmail.com>

# Install phalconphp with php7
RUN apt-get update -y && \
	apt-get install curl -y && \
	curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash && \
	apt-get install php7.0-phalcon && \
	apt-get clean && \
	rm -rf \var\lib\lists\* && \
	echo "extension=phalcon.so" >> /etc/php/7.0/cli/conf.d/20-phalcon.ini