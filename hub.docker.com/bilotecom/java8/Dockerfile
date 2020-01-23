FROM centos:7

MAINTAINER Bilot

ADD jdk-8u161-linux-x64.tar.gz /usr/lib/jvm

ENV JDK_VERSION=1.8.0_161
ENV JAVA_HOME=/usr/lib/jvm/jdk$JDK_VERSION

RUN yum update -y && yum clean all && \
    update-alternatives --install /usr/bin/java java $JAVA_HOME/bin/java 1 && \
    update-alternatives --install /usr/bin/javac javac $JAVA_HOME/bin/javac 1

RUN yum install -y gettext
