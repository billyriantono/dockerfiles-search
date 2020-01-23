# name: 0718c7bf/java8
# version: 1.0
# description: Creates an Ubuntu 14.04 server with oracle Java 8 Debian node running Tomcat6 with Java 8

FROM    ubuntu:14.04
MAINTAINER Mads Hvelplund <mhvelplund@gmail.com>

RUN apt-get -qq update
RUN apt-get -qq -y install software-properties-common
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get -qq update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get -qq -y install oracle-java8-installer
RUN apt-get -qq clean
RUN echo "JAVA_HOME=/usr/lib/jvm/java-8-oracle" >> /etc/environment
