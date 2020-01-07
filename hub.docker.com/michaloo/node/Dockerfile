# michaloo/node
#
# VERSION               0.0.1

FROM ubuntu:14.04

MAINTAINER Michal Raczka me@michaloo.net


RUN echo 'deb http://ppa.launchpad.net/chris-lea/node.js/ubuntu trusty main' > /etc/apt/sources.list.d/nodejs.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C7917B12 \
    && apt-get update -y \
    && apt-get install nodejs -y
