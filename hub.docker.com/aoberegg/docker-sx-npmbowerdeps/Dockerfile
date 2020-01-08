FROM ubuntu:16.04

RUN mkdir -p /Frontend/web

COPY package.json /Frontend/web/package.json
COPY bower.json /Frontend/web/bower.json

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

RUN apt-get install -y nodejs nodejs-legacy
RUN apt-get install -y npm
RUN apt-get install -y git
RUN apt-get install -y nginx
RUN npm install -g bower
RUN npm install -g gulp

RUN cd /Frontend/web && ls && npm install && bower install --allow-root && cd ~

