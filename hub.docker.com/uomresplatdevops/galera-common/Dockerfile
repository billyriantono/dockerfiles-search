FROM ubuntu:14.04
MAINTAINER Tim Dettrick <t.dettrick@uq.edu.au>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -y install software-properties-common && \
  apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db && \
  add-apt-repository 'deb http://mirror.aarnet.edu.au/pub/MariaDB/repo/10.0/ubuntu trusty main' && \
  apt-get update -y && \
  apt-get clean

RUN groupadd --gid 330 -r mysql && useradd --uid 330 -r -g mysql mysql
