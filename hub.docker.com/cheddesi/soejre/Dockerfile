FROM amazonlinux:latest
MAINTAINER Siva Chedde (cheddesi@gmail.com)
ENV REFRESHED_AT 2017-08-08

#Install wget
RUN yum -y install wget
#Download and Install Oracle Jdk 8
RUN wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jre-8u144-linux-x64.tar.gz
RUN mkdir -p /usr/lib/jvm
RUN tar -zxf jre-8u144-linux-x64.tar.gz -C /usr/lib/jvm
RUN update-alternatives --install /usr/bin/java java /usr/lib/jvm/jre1.8.0_144/bin/java 100
RUN update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jre1.8.0_144/bin/javac 100
ENV JAVA_HOME /usr/lib/jvm/jre1.8.0_144
#RUN export PATH=$PATH:$JAVA_HOME/bin
RUN rm jre-8u144-linux-x64.tar.gz

#This volume is meant to be a readonly place holder for all configuration files of the application. 
VOLUME /config
#This volume is meant to be a read-write or persistent volume for any data that application wants to store.
VOLUME /data
