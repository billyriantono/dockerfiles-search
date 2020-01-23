FROM centos:7

# File Author / Maintainer
MAINTAINER Jonathan Farbiarz <jonathan.farbiarz@group-label.com>

ENV HTTP_PORT 1080
ENV SMTP_PORT 1025

RUN yum clean all
RUN yum -y update
RUN yum -y install gcc gcc-c++
RUN yum -y install ruby
RUN yum -y install ruby-devel
RUN yum -y install make automake autoconf curl-devel sqlite-devel
RUN yum -y install rubygems
RUN gem install mailcatcher

EXPOSE 1080 1025