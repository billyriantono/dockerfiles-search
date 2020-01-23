FROM centos
MAINTAINER Marvin Liao <coldljy@gmail.com>

ENV JAVA_VERSION 8u172
ENV BUILD_VERSION b11
ENV DOWNLOAD_LINK "http://download.oracle.com/otn-pub/java/jdk/8u172-b11/a58eab1ec242421181065cdc37240b08/jre-8u172-linux-x64.rpm"

# Upgrading system
RUN yum -y update && \
    yum -y install wget && \
    wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=xxx; oraclelicense=accept-securebackup-cookie" "$DOWNLOAD_LINK" -O /tmp/jre-8-linux-x64.rpm && \
    yum -y install /tmp/jre-8-linux-x64.rpm && \
    rm -f /tmp/jre-8-linux-x64.rpm && \
    yum clean all

ENV JAVA_HOME /usr/java/latest