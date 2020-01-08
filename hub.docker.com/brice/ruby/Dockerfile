FROM ubuntu:14.04
MAINTAINER Brandon Rice <brice84@gmail.com>

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install wget gcc make libssl-dev libreadline-dev zlibc 
RUN wget http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz
RUN tar xzvf ruby-2.1.2.tar.gz
RUN cd ruby-2.1.2 && ./configure --disable-install-doc
RUN cd ruby-2.1.2 && make install
