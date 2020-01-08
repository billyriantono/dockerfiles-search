FROM ubuntu:latest
MAINTAINER Galileo Martinez "playgali@gmail.com"
ENV REFRESHED_AT 2018-Jun-08
ENV CHEF_VERSION 12.20.3

RUN apt-get update && apt-get install curl nano vim -y \
 && curl -L https://www.opscode.com/chef/install.sh | bash -s -- -v $CHEF_VERSION
