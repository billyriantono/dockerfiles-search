FROM centos:7
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN yum -y install wget
RUN yum -y install java

RUN yum -y install httpd php php-gd
RUN yum -y install initscripts

RUN yum -y install gcc openssl-devel bzip2-devel

RUN yum -y install python

RUN yum -y install make gcc-c++ 

RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -
RUN yum -y install nodejs
