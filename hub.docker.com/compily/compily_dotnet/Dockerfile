FROM ubuntu:14.04
MAINTAINER Ephraim Rothschild
RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode

# Update the repository sources list
#RUN echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y


# For C#
RUN apt-get install -y mono-xsp2
RUN apt-get install -y mono-xsp2-base

# For VB.NET
RUN apt-get install -y mono-vbnc

RUN apt-get install -y bc
