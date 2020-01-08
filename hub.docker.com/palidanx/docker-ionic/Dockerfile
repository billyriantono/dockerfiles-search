FROM ubuntu:18.04

ENV IONIC_VERSION 4.5.0

RUN apt update
RUN apt-get -y install vim
RUN apt-get -y install nano
RUN apt-get install -y curl 
RUN apt-get install -y gnupg2 
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y gcc g++ build-essential make
RUN apt-get install -y nodejs
RUN apt-get install -y git
RUN npm i -g ionic
RUN npm install -g cordova

EXPOSE  8100


