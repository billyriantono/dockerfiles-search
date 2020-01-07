FROM centos:6

MAINTAINER kter <me@kter.jp>

RUN yum -y update

RUN yum install -y gcc tar dbm-devel gdbm-devel openssl-devel readline-devel tk-devel zlib-devel

WORKDIR /usr/local/src

RUN curl https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.1.tar.gz | tar zx && cd ruby-2.3.1 && ./configure && make install

WORKDIR /
