# Getting Base Image
FROM centos:6.7

# Author Info
MAINTAINER kurebio

# build 時に実行すること
RUN yum update -y
RUN yum upgrade -y
RUN yum -y install epel-release
RUN yum -y install byobu curl tree wget iftop git gcc gcc-c++ libxml2-devel libxslt-devel sqlite-devel --enablerepo=epel
# ruby用
RUN yum -y install openssl-devel readline-devel zlib-devel libcurl-devel bzip2 tar --enablerepo=epel

# タイムゾーンを日本に設定
RUN \cp -fp /usr/share/zoneinfo/Japan /etc/localtime

# nginx
RUN rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm
RUN yum -y install nginx --enablerepo=epel

RUN yum -y install http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm
RUN yum -y install yum-utils
RUN yum-config-manager --disable mysql56-community
RUN yum-config-manager --enable mysql57-community-dmr
RUN yum install -y mysql mysql-devel mysql-utilities

# Node
RUN yum -y install nodejs npm --enablerepo=epel

# copy local file
ADD config/ /home/config/
ADD www/ /home/www/
RUN \cp -f /home/config/nginx.conf /etc/nginx/nginx.conf

# Ruby
RUN chmod u+x /home/config/install_ruby.sh
RUN /home/config/install_ruby.sh

# Port
EXPOSE 80

CMD ["/bin/bash"]
