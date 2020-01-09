# Uses official centos puppetlabs image
FROM centos

MAINTAINER piwi3910<pascal.watteel@emc.com>

# Environment variables 
ENV NIFI_VERSION 0.6.1
ENV NIFI_HOME /usr/local/lib/nifi/nifi-${NIFI_VERSION}

ENV JAVA_HOME /usr/lib/jvm/java-openjdk

# prerequirements
RUN yum install -y epel-release
RUN yum install -y wget
RUN wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
RUN yum remove -y maven* *mvn* *plexus*

RUN yum install -y aria2 openjdk-7-jdk git tar apache-maven

# Download and install Nifi from a mirror
RUN mkdir -p /usr/local/lib/nifi && aria2c -x 16 -s 16 http://www.eu.apache.org/dist/nifi/${NIFI_VERSION}/nifi-${NIFI_VERSION}-bin.tar.gz -d /usr/local/lib/nifi
RUN tar xzf /usr/local/lib/nifi/nifi-${NIFI_VERSION}-bin.tar.gz -C /usr/local/lib/nifi
RUN rm /usr/local/lib/nifi/nifi-${NIFI_VERSION}-bin.tar.gz

# Add Nifi to PATH
ENV PATH $PATH:$NIFI_HOME/bin

RUN echo "#!/bin/bash" > start.sh && echo "nifi.sh start" >> start.sh 
RUN bash start.sh

# Expose Nifi default port 8080
EXPOSE 8080
