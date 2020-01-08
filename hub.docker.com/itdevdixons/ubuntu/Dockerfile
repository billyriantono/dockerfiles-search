FROM ubuntu:14.04

MAINTAINER Viliam Husar viliam.husar@dixonscarphonegroup.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y install mc nano curl apt-transport-https

# Install confd
ADD libraries/confd-0.6.3-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd

