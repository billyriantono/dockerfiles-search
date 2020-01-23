FROM centos:centos7
MAINTAINER Mehul Bhatt <mehulsbhatt@hotmail.com> <https://mehulbhatt.com> <@mehulbhatt>
## Update system
RUN yum update -y
RUN yum install -y wget
RUN yum install -y unzip
RUN yum install -y tar
RUN yum clean -y all
## Download and install OracleJDK 1.8 (Java SE Development Kit 8u60)
RUN cd /tmp && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"  http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-x64.tar.gz
RUN tar -zxf /tmp/jdk-8u60-linux-x64.tar.gz -C /opt
RUN rm -rf /tmp/jdk-8u60-linux-x64.tar.gz
RUN ln -s /opt/jdk1.8.0_60  /opt/java
RUN alternatives --install /usr/bin/java java /opt/jdk1.8.0_60/bin/java 2
RUN alternatives --install /usr/bin/jar jar /opt/jdk1.8.0_60/bin/jar 2
RUN alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_60/bin/javac 2
RUN alternatives --set jar /opt/jdk1.8.0_60/bin/jar
RUN alternatives --set javac /opt/jdk1.8.0_60/bin/javac
## Set up Java environment variables
ENV JAVA_HOME /opt/java
ENV JRE_HOME /opt/java/jre
ENV PATH ${PATH}:${JAVA_HOME}/bin:${JRE_HOME}/bin
