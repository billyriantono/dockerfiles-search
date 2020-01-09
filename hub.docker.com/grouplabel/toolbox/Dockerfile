FROM debian:jessie
MAINTAINER GroupLabel Development <tech@group-label.com>

RUN apt-get update && apt-get upgrade
RUN apt-get -y install supervisor openssh-client tar
RUN apt-get -y install mysql-client
RUN apt-get -y install rsync
RUN apt-get -y install git

RUN mkdir /tmp/dump
RUN mkdir /tmp/magento
RUN mkdir /tmp/locks