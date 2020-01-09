FROM centos:6

MAINTAINER Jindřich Káňa <jindrich.kana@gmail.com>
LABEL Vendor="Demo pro T-Mobile"

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm \
        &&  yum -y --setopt=tsflags=nodocs update \
	&& yum --setopt=tsflags=nodocs -y install \
	gcc \
	gcc-c++ \
	httpd \
	mod_ssl \
	php \
	php-cli \
	php-devel \
	php-mysql \
	php-pdo \
	php-mbstring \
	php-soap \
	php-gd \
	php-xml \
	php-pecl-apcu \
	libXrender fontconfig libXext urw-fonts \
	&& rm -rf /var/cache/yum/* \
        && yum clean all
