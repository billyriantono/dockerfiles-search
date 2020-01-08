# Ruby on CentOS6
FROM centos:centos6
LABEL maintainer="akahigeg@gmail.com"
 
# install packages for Rails and more...
RUN yum -y update && yum -y install gcc gcc-c++ libxml2-devel libxslt-devel openssl-devel readline-devel mysql-devel wget

# install Ruby and Bundler
ENV RUBY_VERSION 2.3.4
ENV CONFIGURE_OPTS --disable-install-doc
RUN wget https://cache.ruby-lang.org/pub/ruby/2.3/ruby-$RUBY_VERSION.tar.bz2
RUN tar jxf ruby-$RUBY_VERSION.tar.bz2
RUN cd ruby-$RUBY_VERSION && ./configure && make && make install
RUN gem install bundler

