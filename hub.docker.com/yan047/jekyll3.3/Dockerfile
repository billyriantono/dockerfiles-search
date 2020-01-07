# Version: 1.0
# NAME: jekyll3.3
FROM ubuntu:16.04

MAINTAINER "boyan.au@gmail.com"

# In case someone loses the Dockerfile
RUN rm -rf /etc/Dockerfile
ADD Dockerfile /etc/Dockerfile

ENV DEBIAN_FRONTEND noninteractive
ENV WORK_BASE=/jekyll

RUN apt-get update && \ 
	apt-get -y install ruby ruby-dev make gcc wget unzip curl git vim && \
	apt-get clean

RUN yes | gem install jekyll -v3.3.1 && \
	yes | gem install bundler

RUN mkdir -p $WORK_BASE
WORKDIR $WORK_BASE
EXPOSE 35729
EXPOSE 4000

