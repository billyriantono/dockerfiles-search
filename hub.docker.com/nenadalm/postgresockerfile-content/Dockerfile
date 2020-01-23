# Version: 0.0.1
# Node, mongo
FROM ubuntu:14.04
MAINTAINER Nathan Samano "nsv9982@saintjoe.edu"
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y vim
RUN echo 'Installed vim'
RUN apt-get install -y curl
RUN apt-get install -y git
RUN git clone https://github.com/nathansamano/MyFinishedBookCodeSPA.git
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -
RUN apt-get install -y nodejs
RUN curl -O http://downloads.mongodb.org/linux/mongodb-linux-x86_64-2.6.4.tgz
RUN tar -zxvf mongodb-linux-x86_64-2.6.4.tgz
RUN mkdir -p mongodb
RUN cp -R -n mongodb-linux-x86_64-2.6.4/ mongodb
RUN export PATH=~/mongodb/mongod-linux-x86_64-2.6.4/bin:$PATH
RUN mkdir -p /data/db
RUN chmod 777 /data
RUN echo 'You may now run mongod --fork --syslog to start mongo'
