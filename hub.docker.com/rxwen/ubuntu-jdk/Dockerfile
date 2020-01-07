FROM ubuntu:16.04

MAINTAINER Raymond Wen "rx.wen218@gmail.com"

ENV JAVA_HOME /opt/jdk
RUN apt-get update && apt-get install -y wget curl unzip zip
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.tar.gz" -O jdk.tar.gz
RUN tar -C /opt/ -xf jdk.tar.gz && rm jdk.tar.gz && mv /opt/jdk1.8.0_144 /opt/jdk
ENV PATH $PATH:$JAVA_HOME/bin
# Cleaning
RUN apt-get clean
