FROM ubuntu:16.04
MAINTAINER Ephraim Rothschild
RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode

# Update the repository sources list
RUN echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y php7.0-cli

RUN apt-get install -y bc
