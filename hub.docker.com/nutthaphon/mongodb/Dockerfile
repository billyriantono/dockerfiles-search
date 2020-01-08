FROM ubuntu:xenial
MAINTAINER Nutthaphon Suwanwong

RUN (mv /etc/localtime /etc/localtime.old; ln -s /usr/share/zoneinfo/Asia/Bangkok /etc/localtime)

RUN echo deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/testing multiverse >> /etc/apt/sources.list.d/mongodb-org-3.4.list

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
RUN apt-get update

RUN apt-get install -y mongodb-org


COPY xenial/mongod.service /lib/systemd/system
COPY xenial/mongod.conf /etc
COPY startup.sh .

RUN chmod +x startup.sh

EXPOSE 27017

CMD "./startup.sh"
