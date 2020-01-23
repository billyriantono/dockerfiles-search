FROM centos:7

LABEL author="cuihairu <chuihairu@gmail.com>"

ADD http://mirrors.aliyun.com/repo/Centos-7.repo /etc/yum.repos.d/CentOS-Base.repo

RUN yum update -y \
    && yum install -y java-1.8.0-openjdk-* unzip zip \
    && yum clean all \
    && rm -rf /var/cache/yum/*

ENV JAVA_HOME /etc/jdk
ENV CLASSPATH $CLASSPATH:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar:${ANT_HOME}/lib
ENV PATH $PATH:$JAVA_HOME/bin:$ANT_HOME/bin