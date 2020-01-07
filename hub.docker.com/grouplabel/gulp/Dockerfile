# Set the base image to centos
FROM centos:7

# File Author / Maintainer
MAINTAINER Jonathan Farbiarz <jonathan.farbiarz@group-label.com>

# Add the nginx and PHP dependent repository
RUN yum clean all
RUN yum -y update
RUN yum -y install epel-release
RUN yum -y install nodejs npm
RUN yum -y install ruby
RUN yum -y install gcc g++ make automake autoconf curl-devel openssl-devel zlib-devel httpd-devel apr-devel apr-util-devel sqlite-devel
RUN yum -y install ruby-rdoc ruby-devel
RUN yum -y install rubygems
RUN gem install compass --pre

RUN npm cache clean -f
RUN npm install -g n
RUN n stable
RUN npm install -g gulp
RUN npm install gulp
RUN npm install gulp-watch
RUN npm install gulp-compass
RUN npm install path
RUN npm install del
RUN npm install gulp-imagemin