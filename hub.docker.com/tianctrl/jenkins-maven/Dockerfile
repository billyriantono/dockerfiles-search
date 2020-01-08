FROM jenkins:1.651.3
MAINTAINER tianh

USER root

ENV MAVEN_VERSION 3.3.9
ENV MAVEN_HOME /usr/local/maven

RUN curl -O http://www-eu.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz
RUN tar -xzf apache-maven-$MAVEN_VERSION-bin.tar.gz -C /usr/local
RUN mv /usr/local/apache-maven-$MAVEN_VERSION /usr/local/maven
RUN ln -s /usr/local/maven/bin/mvn /usr/local/bin/mvn