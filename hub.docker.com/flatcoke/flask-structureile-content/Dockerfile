# official image name: cscope/sti-builder-java-maven-base
FROM openshift/base-centos7

MAINTAINER Kirill Frolov <kirill.frolov@servian.com>

ENV BUILDER_VERSION 1.0

RUN wget http://apache.uberglobalmirror.com/maven/maven-3/3.3.3/binaries/apache-maven-3.3.3-bin.tar.gz \
 && tar zxvf apache-maven-3.3.3-bin.tar.gz \
 && mkdir -p /opt/maven \
 && mv apache-maven-3.3.3/* /opt/maven/ \
 && rm -Rf apache-maven-3.3.3* \
 && ln -s /opt/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME=/opt/maven

RUN yum install -y java-1.8.0-openjdk-devel && yum clean all -y

USER 1001
