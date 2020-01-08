# DOCKER-VERSION 0.6.4

FROM ubuntu:12.04

RUN echo deb http://archive.ubuntu.com/ubuntu precise main universe multiverse > /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y python-software-properties
RUN add-apt-repository -y ppa:chris-lea/redis-server
RUN apt-get update
RUN apt-get install -y redis-server

EXPOSE 6379

ENTRYPOINT ["/usr/bin/redis-server"]
