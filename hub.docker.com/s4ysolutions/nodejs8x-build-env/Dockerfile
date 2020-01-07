# Set the base image to Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER Sergey Dolin <sergey@s4y.solutions>
RUN apt-get update \
  && apt-get install -y  curl git docker.io python-pip \
  && curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh \
  && /bin/bash nodesource_setup.sh \
  && apt-get install nodejs \
	&& rm -rf /var/lib/apt/lists/* 

RUN pip install "docker-compose==1.8.0"
RUN pip install awscli --upgrade --user
