# Dockerfile

FROM  ubuntu:latest
#FROM  alpine:latest

MAINTAINER  Author Name <ccancellieri@hotmail.com>

RUN apt-get -y update
RUN apt-get -y install npm maven

ENV JAVA_VER 8
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle/

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-get install -y debconf-utils
RUN apt-get install -y openssh-client
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get install -y oracle-java8-installer;
RUN apt-get install -y oracle-java8-set-default
#RUN update-java-alternatives -s java-8-oracle
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-oracle/" >> ~/.bashrc


