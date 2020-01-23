FROM ubuntu:16.04
MAINTAINER Adi Priyanto "adipriyanto.bpn@gmail.com"
ENV REFRESHED_AT 2016-08-23 04:19

RUN apt-get update
RUN apt-get install apt-transport-https ca-certificates -y
RUN echo deb https://apt.dockerproject.org/repo ubuntu-xenial main >> /etc/apt/sources.list.d/docker.list
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

RUN apt-get update
RUN apt-get install docker-engine -y 
RUN apt-get install curl lynx nano -y
