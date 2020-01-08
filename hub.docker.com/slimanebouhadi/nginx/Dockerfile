FROM ubuntu:16.04
MAINTAINER Slimane Bouhadi <slimane.bouhadi@gmail.com>
#=================================
# Customize sources for apt-get
#=================================
#RUN  echo "deb http://archive.ubuntu.com/ubuntu vivid main universe\n" > /etc/apt/sources.list \
#  && echo "deb http://archive.ubuntu.com/ubuntu vivid-updates main universe\n" >> /etc/apt/sources.list

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
#=================================
# Install all dependencies
#=================================

RUN apt-get update && \

 apt-get -y  install nginx

#================================

#WORKDIR $HOME


EXPOSE 8080

#==========================
# Run nginx as default
#==========================
CMD nginx

