FROM ubuntu:14.04
MAINTAINER @icojo
RUN sudo apt-get update  
RUN sudo apt-get -y install software-properties-common
  	
RUN \
  	sudo add-apt-repository ppa:webupd8team/java && \
  	sudo apt-get update

RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN sudo apt-get -y install oracle-java8-set-default && \
	sudo apt-get clean
