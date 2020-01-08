FROM ubuntu:14.04.2
MAINTAINER cannin

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y mongodb

RUN mkdir -p /data/db

EXPOSE 27017

CMD ["mongod"]

