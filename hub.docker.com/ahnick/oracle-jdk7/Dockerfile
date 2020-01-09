FROM stackbrew/ubuntu:precise
MAINTAINER Xan Nick "xan.nick@gmail.com"

RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y python-software-properties
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN apt-get upgrade -y

RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y oracle-java7-installer
RUN apt-get autoremove && apt-get autoclean
RUN update-alternatives --display java
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
