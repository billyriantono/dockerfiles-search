FROM ubuntu:16.04

MAINTAINER pamtrak06 <pamtrak06@gmail.com>
ENV REFRESHED_ON "08 Oct 2016"

RUN apt-get update && apt-get -y install git

WORKDIR /opt
RUN git clone https://github.com/OpenVPN/easy-rsa.git
WORKDIR /opt/easy-rsa
RUN git pull origin master --tags
RUN git checkout 3.0.1
WORKDIR /opt/easy-rsa/easyrsa3
