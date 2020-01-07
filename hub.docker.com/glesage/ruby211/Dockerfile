# Ruby environment
#
# VERSION               0.1

FROM ubuntu:12.04
MAINTAINER Geoffroy Lesage

RUN apt-get update
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get -q -y install build-essential zlib1g-dev libssl-dev libreadline6-dev libyaml-dev

ADD http://ftp.ruby-lang.org/pub/ruby/2.1/ruby-2.1.1.tar.gz /tmp/

RUN cd /tmp && \
    tar -xzf ruby-2.1.1.tar.gz && \
    cd ruby-2.1.1 && \
    ./configure && \
    make && \
    make install && \
    cd .. && \
    rm -rf ruby-2.1.1 && \
    rm -f ruby-2.1.1.tar.gz\
    echo "gem: --no-ri --no-rdoc" > ~/.gemrc