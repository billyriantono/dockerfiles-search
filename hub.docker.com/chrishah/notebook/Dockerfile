FROM ubuntu:14.04

MAINTAINER Christoph Hahn <chrisi.hahni@gmail.com>

RUN apt-get update
RUN apt-get upgrade -y

# Not essential, but wise to set the lang (taken from szitenberg/reprophylo)
RUN apt-get install -y language-pack-en
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

# basic tools
RUN apt-get install -y git vim perl

RUN mkdir /home/src
VOLUME /home/data
WORKDIR /home
RUN chmod -R a+rw /home

