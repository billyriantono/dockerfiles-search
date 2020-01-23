#Source image - Ubuntu 16.04
FROM ubuntu:16.04

#Install common soft
RUN apt-get update && apt-get install -y \
	git

#Install Node.js related soft
RUN apt-get update && apt-get install -y \
	nodejs-legacy \
	npm \
	build-essential

#Install aws_cli
RUN apt-get update && apt-get install -y \
	python-dev \
	python-pip
RUN python -m pip install --upgrade pip --user && python -m pip install awscli --upgrade --user

RUN mkdir /src
WORKDIR /src