FROM debian:wheezy
MAINTAINER Ryosuke Akiyama <ryosuke.akiyama@broadleaf.co.jp>

RUN apt-get update && apt-get upgrade -y -q
RUN apt-get install --no-install-recommends -y -q build-essential libyaml-dev libssl-dev libgdbm-dev libqdbm-dev libreadline6-dev libncurses5-dev libffi-dev libz-dev libgmp-dev curl autoconf ca-certificates systemtap

RUN mkdir -p /usr/src && curl -L http://ftp.ruby-lang.org/pub/ruby/2.1/ruby-2.1.5.tar.bz2 | tar -C /usr/src -xj
RUN cd /usr/src/ruby-2.1.5 && autoconf && ./configure --prefix=/usr --disable-install-doc && make && make install && make clean
RUN gem install -q --no-rdoc --no-ri bundler --version 1.8.0
