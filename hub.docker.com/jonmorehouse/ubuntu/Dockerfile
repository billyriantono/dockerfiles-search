FROM ubuntu:quantal
MAINTAINER Jon Morehouse <morehousej09@gmail.com>

# dependency management
RUN apt-get update 
RUN DEBIAN_FRONTEND=noninteractive apt-get -y upgrade 
RUN DEBIAN_FRONTEND=noninteractive 
RUN apt-get install -y make \
	gcc \
	git \
	curl \
	python-software-properties \
	python \
	zsh \
	cgroup-lite \
	g++ 


