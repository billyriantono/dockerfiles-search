##############################################################
# Dockerfile to build Recipe Management Service Mongo Database
# Based on ubuntu:16.04
##############################################################

FROM ubuntu:16.04

MAINTAINER Erik Hage <ehage4@gmail.com>

ENV TERM xterm

#Install text editor nano
RUN ["apt-get", "update"]
RUN ["apt-get", "install", "-y", "nano"]

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
RUN echo "deb http://repo.mongodb.org/apt/ubuntu $(cat /etc/lsb-release | grep DISTRIB_CODENAME | cut -d= -f2)/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list

# Update apt-get sources AND install MongoDB
RUN apt-get update && apt-get install -y mongodb-org

RUN mkdir -p /data/db

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]