FROM ubuntu:18.04

RUN export DEBIAN_FRONTEND=noninteractive 
RUN apt-get --assume-yes update 
RUN apt-get --assume-yes install locales ca-certificates wget curl git zip ruby ruby-dev build-essential gnupg2

RUN  curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get --assume-yes install nodejs
RUN npm install -g gulp-cli
RUN npm install -g bower
RUN gem install compass