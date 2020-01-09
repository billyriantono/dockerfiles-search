FROM ubuntu:16.04
MAINTAINER Andruby

RUN apt-get update
RUN apt-get -y install  git automake build-essential  libcurl4-openssl-dev libncurses5-dev pkg-config automake yasm

RUN cd /opt ; git clone https://github.com/OhGodAPet/cpuminer-multi.git
RUN cd /opt/cpuminer-multi ; ./autogen.sh
RUN cd /opt/cpuminer-multi ; CFLAGS="-march=native" ./configure
RUN cd /opt/cpuminer-multi ; make
RUN cd /opt/cpuminer-multi ; make install
