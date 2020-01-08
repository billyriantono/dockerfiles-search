FROM centos:7
MAINTAINER Gsviec <hello@gsviec.com>
ENV container docker

RUN yum install epel-release -y

RUN yum install gcc libxml2-devel libXpm-devel gmp-devel libicu-devel \
t1lib-devel aspell-devel openssl-devel bzip2-devel libcurl-devel \
libjpeg-devel libvpx-devel libpng-devel freetype-devel readline-devel \
libtidy-devel libxslt-devel libmcrypt-devel pcre-devel curl-devel \
mysql-devel ncurses-devel gettext-devel net-snmp-devel libevent-devel \
libtool-ltdl-devel libc-client-devel postgresql-devel bison gcc make wget -y


RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
