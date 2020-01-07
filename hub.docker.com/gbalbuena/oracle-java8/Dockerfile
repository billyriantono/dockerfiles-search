FROM ubuntu:16.04

LABEL maintainer="gabrielbalbuena@gmail.com"
LABEL version="1.0"

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y dnsutils
RUN apt-get install -y oracle-java8-installer
RUN apt-get install -y ca-certificates
RUN apt-get install -y maven
