FROM centos:7
MAINTAINER Gene Liverman "me@technicalissues.us"

RUN yum -y install gcc gcc-c++ make ruby ruby-devel rubygem-bundler
ENV APP_HOME /myapp
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
