FROM ubuntu:14.04

MAINTAINER luyi

RUN apt-get install -y wget

RUN wget --no-cookies \
--no-check-certificate \
--header "Cookie: oraclelicense=accept-securebackup-cookie" \
"http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jdk-8u45-linux-x64.tar.gz" \
-O /usr/local/jdk-8u45-linux-x64.gz


RUN cd /usr/local; tar xf jdk-8u45-linux-x64.gz ; rm jdk-8u45-linux-x64.gz

RUN wget "http://www.scala-lang.org/files/archive/scala-2.11.6.tgz" -O /usr/local/scala-2.11.6.tgz

RUN cd /usr/local; tar xf scala-2.11.6.tgz ; rm scala-2.11.6.tgz

ENV JAVA_HOME /usr/local/jdk1.8.0_45
ENV SCALA_HOME /usr/local/scala-2.11.6
ENV PATH $JAVA_HOME/bin:$SCALA_HOME/bin:$PATH
