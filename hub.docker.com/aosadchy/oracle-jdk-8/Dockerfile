FROM ubuntu:14.04

MAINTAINER Alexandr Osadchy <alexandr.osadchy@gmail.com>

RUN apt-get update && apt-get install -y wget xz-utils && mkdir -p /usr/lib/jvm && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O - http://download.oracle.com/otn-pub/java/jdk/8u51-b16/jdk-8u51-linux-x64.tar.gz | tar -xzC /usr/lib/jvm && mv /usr/lib/jvm/jdk1.8.0_51 /usr/lib/jvm/oracle-jdk-8

ENV J2SDKDIR /usr/lib/jvm/oracle-jdk-8

ENV J2REDIR /usr/lib/jvm/oracle-jdk-8/jre

ENV JAVA_HOME /usr/lib/jvm/oracle-jdk-8

ENV DERBY_HOME /usr/lib/jvm/oracle-jdk-8/db

ENV PATH /usr/lib/jvm/oracle-jdk-8/bin:/usr/lib/jvm/oracle-jdk-8/db/bin:/usr/lib/jvm/oracle-jdk-8/jre/bin:$PATH
