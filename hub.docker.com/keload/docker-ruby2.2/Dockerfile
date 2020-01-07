FROM ubuntu:14.04
MAINTAINER Clément BERARD <keload@gmail.com>
ENV LAST_CHANGED 2014-01-14T13:06EST

# make sure the package repository is up to date
RUN apt-get -y update

# install python-software-properties (so you can do add-apt-repository)
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q python-software-properties software-properties-common

# add brightbox's repo, for ruby2.2
RUN apt-add-repository ppa:brightbox/ruby-ng
RUN apt-get -y update

# install ruby2.2
RUN apt-get -y install ruby2.2 ruby2.2-dev bundler javascript-common

RUN gem update --system

RUN gem install compass

RUN apt-get install git -y

RUN apt-get install nodejs -y

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN apt-get install npm -y

RUN npm install -g grunt grunt-cli

RUN npm install -g bower
