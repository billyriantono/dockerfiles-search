FROM ubuntu:14.04.4

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y install git curl python-dev python-pip libmysqlclient-dev build-essential python-software-properties libfreetype6-dev libjpeg-dev libssl-dev libffi-dev
RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -

RUN apt-get -y install nodejs
RUN npm config set strict-ssl false
RUN npm install -g uglify-js bless bluebird any-promise mz
