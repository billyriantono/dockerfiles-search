# debian wheezy + java 7u71
# 
# VERSION 0.0.4

# 0.0.1 : initial file with centos 6.4 and java 7u60
# 0.0.2 : change centos from 6.4 to 6 and java 7u60 to 7u71
# 0.0.3 : take only necessary in jdk (jre+tools.jar) : reduce image size from 580.4MB to 449.6MB, add JAVA_HOME env
# 0.0.4 : change to debian:wheezy in order to reduce image size (449.6MB->269.4MB)

FROM debian:wheezy

MAINTAINER Samuel Nasello <samuel.nasello@elosi.com>

RUN apt-get update \
	&& apt-get install -y curl tar \
	&& (curl -s -k -L -C - -b "oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.tar.gz | tar xfz - -C /opt) \
	&& mv /opt/jdk1.7.0_71/jre /opt/jre1.7.0_71 \
	&& mv /opt/jdk1.7.0_71/lib/tools.jar /opt/jre1.7.0_71/lib/ext \
	&& rm -Rf /opt/jdk1.7.0_71 \
	&& ln -s /opt/jre1.7.0_71 /opt/java

# Set JAVA_HOME
ENV JAVA_HOME /opt/java
