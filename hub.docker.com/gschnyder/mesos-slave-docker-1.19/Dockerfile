FROM mesoscloud/mesos-slave:0.23.0-ubuntu-14.04

MAINTAINER German Schnyder <gschnyder@gmail.com>

ENV DEBIAN_FRONTEND noninteractive 
ENV SHELL /bin/bash

RUN apt-get -y purge docker-engine
RUN apt-get -y autoremove --purge docker-engine
RUN rm -rf /var/lib/docker

RUN apt-get update
RUN apt-get -y install wget nano
RUN apt-get -y install linux-image-extra-4.4.0-13-generic
RUN apt-get -y install apparmor
RUN apt-get -y install docker-engine=1.7.1-0~trusty