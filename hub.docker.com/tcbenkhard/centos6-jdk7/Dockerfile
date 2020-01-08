# CentOS 6 with JDK 1.7
FROM centos:centos6
MAINTAINER Timo Benkhard <tcbenkhard@gmail.com>

RUN yum install -y curl tar \
    && (curl -s -k -L -C - -b "oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.tar.gz | tar xfz - -C /opt)

ENV JAVA_HOME /opt/jdk1.7.0_71
ENV PATH $JAVA_HOME/bin:$PATH