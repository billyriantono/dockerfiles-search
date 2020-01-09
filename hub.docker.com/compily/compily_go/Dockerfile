FROM ubuntu:16.04
MAINTAINER Ephraim Rothschild

# Update the repository sources list
RUN echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN apt-get update

# For GoLang
RUN apt-get install -y golang-go

RUN apt-get install -y bc
