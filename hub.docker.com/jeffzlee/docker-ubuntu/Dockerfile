FROM ubuntu:trusty
MAINTAINER JeffZLee
ENV DEBIAN_FRONTEND noninteractive 
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
RUN apt-get update  && \
    apt-get -y dist-upgrade && \
    apt-get -y install vim curl git wget  && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV MAVEN_VERSION=3.3.3 
ENV MAVEN_HOME=/usr/local/maven 
ENV PATH=$PATH:/usr/bin/mvn 
    


