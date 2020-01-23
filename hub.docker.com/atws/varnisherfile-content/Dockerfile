FROM ubuntu:16.04

MAINTAINER Atsushi Nagase<ngs@oneteam.co.jp>

RUN apt-get update -y && apt-get install -y --no-install-recommends \
  git cmake ninja-build clang python uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config

RUN git config --global http.sslVerify false
RUN git clone https://github.com/apple/swift.git
RUN cd swift && ./utils/update-checkout --clone

RUN cd swift && utils/build-script -r -t
