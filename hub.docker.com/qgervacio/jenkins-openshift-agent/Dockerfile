FROM openshift/jenkins-slave-maven-centos7:latest

LABEL maintainer="Quirino Gervacio <qgervacio@gmail.com>"

USER root

ENV JAVA_HOME /usr/lib/jvm/java   

RUN yum update -y --skip-broken && yum clean all

USER 1001