FROM redbadger/ruby:latest
MAINTAINER Tiago Azevedo @ https://github.com/tabazevedo

RUN \
  add-apt-repository ppa:chris-lea/node.js &&\
  DEBIAN_FRONTEND=noninteractive apt-get update &&\
  DEBIAN_FRONTEND=noninteractive apt-get -y install nodejs

RUN \
  npm install -g gulp &&\
  npm install -g bower &&\
  gem install sass

VOLUME /data
WORKDIR /data