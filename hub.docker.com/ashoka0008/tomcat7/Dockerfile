FROM ubuntu
MAINTAINER ashoka

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install python-software-properties
RUN apt-get -y install software-properties-common
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get -y update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

RUN apt-get update && apt-get -y install oracle-java7-installer

ENV JAVA_HOME /usr/lib/jvm/java-7-oracle

RUN mkdir -p /opt/tomcat
RUN cd /opt/tomcat
RUN wget http://apache.mirrors.tds.net/tomcat/tomcat-7/v7.0.62/bin/apache-tomcat-7.0.62.tar.gz
RUN tar -xf apache-tomcat-7.0.62.tar.gz
EXPOSE 8080
