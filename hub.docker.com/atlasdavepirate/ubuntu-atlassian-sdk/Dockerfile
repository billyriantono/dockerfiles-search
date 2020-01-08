FROM ubuntu:latest

MAINTAINER David Currie <dcurrie@atlassian.com>

WORKDIR /opt

RUN 	echo debconf shared/accepted-oracle-license-v1-1 select true | \
	debconf-set-selections && \
	apt-get update && \ 
	sh -c 'echo "deb https://sdkrepo.atlassian.com/debian/ stable contrib" >>/etc/apt/sources.list' && \ 
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B07804338C015B73 && \ 
	apt-get install -y apt-transport-https software-properties-common && \ 
	add-apt-repository -y ppa:webupd8team/java && \
	apt-get update && \
	apt-get install -y atlassian-plugin-sdk oracle-java8-installer

CMD bash
