FROM ubuntu:14.04

RUN \
  apt-get install --yes software-properties-common && \
  apt-get install --yes python && \
  add-apt-repository --yes ppa:brightbox/ruby-ng && \
  add-apt-repository --yes ppa:chris-lea/node.js && \
  apt-get update && \
  apt-get install --yes vim curl git

RUN \
  apt-get install --yes ruby2.1 ruby2.1-dev bundler && \
  apt-get install --yes libghc-zlib-dev && \
  apt-get install --yes nodejs

RUN locale-gen en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN gem install rake jekyll nokogiri
