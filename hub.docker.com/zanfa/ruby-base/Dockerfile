FROM ubuntu:latest

WORKDIR /tmp

RUN apt-get install -y build-essential vim git-core curl
RUN apt-get install -y bison openssl libreadline6 libreadline6-dev zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev
RUN apt-get install -y libcurl4-openssl-dev libopenssl-ruby apache2-prefork-dev libapr1-dev libaprutil1-dev
RUN apt-get install -y libx11-dev libffi-dev tcl-dev tk-dev


RUN curl -O http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.0.tar.gz
RUN tar -xvf ruby-2.1.0.tar.gz
WORKDIR /tmp/ruby-2.1.0
RUN ./configure
RUN make
RUN make test
RUN make install

RUN gem install bundler