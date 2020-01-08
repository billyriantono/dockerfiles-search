FROM centos:6.7

MAINTAINER miyamoto_ta <miyamoto_ta@zoho.com>

RUN yum -y update
RUN yum -y groupinstall "Base" "Development tools"
RUN yum clean all

RUN groupadd www-data
RUN useradd -d /home/www-data -g www-data -r -s /sbin/nologin www-data
