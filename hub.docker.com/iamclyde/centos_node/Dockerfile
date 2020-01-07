FROM centos:centos7
MAINTAINER iamclyde@gmail.com
RUN yum -y update yum
RUN yum -y install wget tar
RUN wget http://nodejs.org/dist/v0.12.0/node-v0.12.0-linux-x64.tar.gz
RUN tar --strip-components 1 -xzvf node-v* -C /usr/local
RUN rm -f node-v*.tar.gz
