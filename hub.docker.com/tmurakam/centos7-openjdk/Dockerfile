FROM centos:7
MAINTAINER Takuya Murakami <tmurakam@tmurakam.org>

RUN yum update && yum clean all
RUN curl -SLO https://download.java.net/java/early_access/jdk11/8/GPL/openjdk-11-ea+8_linux-x64_bin.tar.gz && tar xzf openjdk*.tar.gz -C /opt && rm openjdk*.tar.gz

ENV JAVA_HOME /opt/jdk-11
ENV PATH $PATH:/opt/jdk-11/bin

