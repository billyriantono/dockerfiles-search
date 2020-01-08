# Centos image
#
# Version 0.1

# Pull from Centos


FROM wmarinho/centos:latest

MAINTAINER Wellington Marinho wpmarinho@globo.com

RUN yum install java-1.7.0-openjdk -y
RUN update-alternatives --display java
RUN echo "JAVA_HOME=/usr/lib/jvm/jre-1.7.0-openjdk.x86_64" > /etc/environment

