FROM centos:latest
MAINTAINER Paul Lewis <paullewis91@gmail.com>

RUN yum install -y rubygems ruby-devel gcc
RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN gem install puppet librarian-puppet