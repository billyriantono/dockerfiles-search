FROM centos:7
MAINTAINER Matthew Zeemann, matthew@zeemann.name

# Build with:
# docker build -t mattzeemann/jdk-oracle-8 .


# Update the system and make sure we have wget
RUN yum -y install wget

# Downloading the RPM from oracle
ENV JAVA_VERSION 8u60
ENV BUILD_VERSION b27
RUN wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_VERSION/jdk-$JAVA_VERSION-linux-x64.rpm" -O /tmp/jdk-8-linux-x64.rpm

# Install the RPM
RUN yum -y install /tmp/jdk-8-linux-x64.rpm
ENV JAVA_HOME /usr/java/latest
