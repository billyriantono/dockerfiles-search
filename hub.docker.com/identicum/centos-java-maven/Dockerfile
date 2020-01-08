FROM identicum/centos-java:latest
MAINTAINER Gustavo J Gallardo <ggallard@identicum.com>

RUN yum -y install wget git

RUN wget https://archive.apache.org/dist/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz -O /tmp/maven.tgz && \
    tar -xvzf /tmp/maven.tgz --directory /usr/share/ && \
    rm -f /tmp/maven.tgz && \
    mv /usr/share/apache-maven-* /usr/share/apache-maven && \
    ln -s /usr/share/apache-maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/apache-maven

RUN mkdir /source
WORKDIR /source
