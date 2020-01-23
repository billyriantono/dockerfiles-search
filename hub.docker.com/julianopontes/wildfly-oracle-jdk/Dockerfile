# Docker image for WildFly project with Oracle JDK

FROM jboss/wildfly
MAINTAINER Juliano Pontes <juliano.pontes@redspark.io>

USER root

RUN yum -y remove java-1.8.0-openjdk-devel.x86_64
RUN yum -y install wget
RUN wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jdk-8u45-linux-x64.rpm -O /tmp/jdk-8u45-linux-x64.rpm
RUN rpm -ivh /tmp/jdk-8u45-linux-x64.rpm
RUN rm /tmp/jdk-8u45-linux-x64.rpm
RUN alternatives --set java /usr/java/jdk1.8.0_45/jre/bin/java

ENV JAVA_HOME /usr/java/jdk1.8.0_45

USER jboss