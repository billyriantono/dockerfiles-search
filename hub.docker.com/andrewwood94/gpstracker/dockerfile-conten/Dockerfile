FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y nodejs npm
RUN apt-get install -y mongodb

WORKDIR /opt/www
RUN npm install express --save
RUN npm install body-parser --save

ADD . /opt/base

EXPOSE 80