FROM redbadger/base:latest

RUN \
  add-apt-repository ppa:chris-lea/node.js &&\
  DEBIAN_FRONTEND=noninteractive apt-get update &&\
  DEBIAN_FRONTEND=noninteractive apt-get -y install nodejs

RUN \
  npm install -g gulp