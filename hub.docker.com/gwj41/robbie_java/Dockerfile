FROM ubuntu:latest
MAINTAINER Wenjun Gu "gwj41@hotmail.com"
ENV REFRESHED_AT 2016-05-04
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_UPDATE 102
RUN mkdir /usr/jdk && \
apt-get update && \
apt-get install -y wget && \
wget -q --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_UPDATE}-b14/jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_UPDATE}-linux-x64.tar.gz
RUN tar -zxvf jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_UPDATE}-linux-x64.tar.gz -C /usr/jdk
EXPOSE 80
ENV JAVA_HOME /usr/jdk/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_UPDATE}
ENV PATH ${PATH}:${JAVA_HOME}/bin
ENV CLASSPATH .:${JAVA_HOME}/lib:${JAVA_HOME}/jre/lib
