# A base image which contains
# For more information; https://github.com/rdpanek/docker_base
#
#
# Usage
#
#

# VERSION 2.0

FROM ubuntu:14.04
MAINTAINER Radim Daniel Panek <rdpanek@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C
ENV HOME /root


# enable universe
RUN sed 's/main$/main universe/' -i /etc/apt/sources.list

# copy & install dependencies
ADD install /tmp/install
RUN chmod +x /tmp/install/*
RUN /tmp/install/dependencies.sh
RUN /tmp/install/prepare.sh
RUN rm /tmp/install -rf

# screen
ADD files/screenrc /root/.screenrc

# add next dependencies
ADD files/.vimrc /root/.vimrc
ADD files/.gitconfig /root/.gitconfig

# start & install
ADD files/install.sh /opt/install.sh
RUN mkdir -p /opt/run
RUN chmod +x /opt/install.sh