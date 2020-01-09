FROM ubuntu:18.04

MAINTAINER <christoph.hahn@uni-graz.at>

RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential vim git wget

#setup kmc3
WORKDIR /usr/bin
RUN wget https://github.com/refresh-bio/KMC/releases/download/v3.0.0/KMC3.linux.tar.gz && \
	tar xvfz KMC3.linux.tar.gz


