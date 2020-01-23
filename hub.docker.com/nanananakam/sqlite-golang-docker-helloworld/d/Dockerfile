FROM ubuntu:trusty
MAINTAINER Tatsuro Hisamori <medianetworks@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales
RUN apt-get update 
RUN apt-get -y install git curl

RUN git clone https://github.com/sstephenson/ruby-build.git /usr/local/src/ruby-build
RUN cd /usr/local/src/ruby-build && ./install.sh

CMD ruby-build --version
