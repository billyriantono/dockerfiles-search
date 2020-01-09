FROM ubuntu:16.04

MAINTAINER <christoph.hahn@uni-graz.at>

RUN apt-get update && apt-get -y upgrade && \
        apt-get install -y build-essential vim git wget 

WORKDIR /usr/src
RUN wget http://www.clustal.org/omega/clustalo-1.2.4-Ubuntu-x86_64 && \
	chmod a+x clustalo-1.2.4-Ubuntu-x86_64 && \
	ln -s $(pwd)/clustalo-1.2.4-Ubuntu-x86_64 /usr/bin/clustalo

#create working directory and move to entrypoint
VOLUME /home/data
WORKDIR /home/data

