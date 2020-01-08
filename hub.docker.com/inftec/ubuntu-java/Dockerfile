# This builds a Ubuntu Docker container with Java installed

FROM ubuntu:18.04
MAINTAINER Fabian Gut <fabian.gut@inftec.ch>, InfTec GmbH
MAINTAINER Martin Meyer <martin.meyer@inftec.ch>, InfTec GmbH

# Java version to be installed
ENV JAVA_VERSION 8u171-1~webupd8~0

# Install required software
RUN apt-get update && \
    apt-get install -y \
        apt-utils \
        software-properties-common

# Add webupd8team ppa
RUN add-apt-repository ppa:webupd8team/java

# Install Oracle Java 8
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | \
        /usr/bin/debconf-set-selections && \
    apt-get update && \
    apt-get install -y \
        oracle-java8-installer=${JAVA_VERSION} && \
    apt-get autoclean
        
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Scripts to deal with (optional) certificate import
RUN mkdir /javacert
COPY assets/importCerts.sh /javacert
