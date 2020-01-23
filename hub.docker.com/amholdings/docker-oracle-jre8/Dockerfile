FROM centos:centos7
MAINTAINER Mehul Bhatt <mehulsbhatt@hotmail.com> <https://mehulbhatt.com> <@mehulbhatt>
## Update system
RUN yum update -y
RUN yum install -y wget
RUN yum install -y unzip
RUN yum install -y tar
RUN yum clean -y all
## Download and install Oracle Java 1.8 (Java SE Runtime Environment 8u60)
RUN cd /tmp && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"  http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jre-8u60-linux-x64.tar.gz
RUN tar -zxf /tmp/jre-8u60-linux-x64.tar.gz -C /opt
RUN rm -rf /tmp/jre-8u60-linux-x64.tar.gz
RUN ln -s /opt/jre1.8.0_60  /opt/java
## Set up Java environment variables
ENV JAVA_HOME /opt/java
ENV PATH ${PATH}:${JAVA_HOME}/bin
