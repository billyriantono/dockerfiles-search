FROM ubuntu:latest
MAINTAINER Dieter Provoost <dieter.provoost@marlon.be>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/mongodb.list
RUN apt-get update

RUN apt-get install -y mongodb-10gen

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo "root:root" | chpasswd

RUN apt-get clean -y

EXPOSE 22
EXPOSE 27017

ADD start.sh start.sh

CMD ["sh", "start.sh"]
