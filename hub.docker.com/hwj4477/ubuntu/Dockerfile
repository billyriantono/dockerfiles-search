FROM ubuntu:14.04

MAINTAINER hwj4477@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# common
RUN apt-get update
RUN apt-get install -y curl

# environment setting
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# tools
RUN apt-get install -y vim
RUN apt-get install -y git
