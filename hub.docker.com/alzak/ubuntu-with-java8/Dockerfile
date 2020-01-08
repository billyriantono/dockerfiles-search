FROM ubuntu:12.04

RUN  apt-get update
RUN  apt-get install python-software-properties -y
RUN  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN  add-apt-repository -y ppa:webupd8team/java
RUN  apt-get update
RUN  apt-get install -y oracle-java8-installer
RUN  rm -rf /var/lib/apt/lists/*
RUN  rm -rf /var/cache/oracle-jdk8-installer

RUN export JAVA_HOME=/usr/lib/jvm/java-8-oracle

RUN mkdir /opt/app