FROM centos:7

LABEL author="cuihairu <chuihairu@gmail.com>"

ADD http://mirrors.aliyun.com/repo/Centos-7.repo /etc/yum.repos.d/CentOS-Base.repo

RUN yum update -y \
    && yum install -y java-1.7.0-openjdk-* unzip zip

ADD https://www-eu.apache.org/dist//ant/binaries/apache-ant-1.9.14-bin.zip /usr/local/

RUN unzip /usr/local/apache-ant-1.9.14-bin.zip -d /usr/local \
    && rm -f /usr/local/apache-ant-1.9.14-bin.zip \
    && mv /usr/local/apache-ant-1.9.14 /usr/local/ant \
    && yum clean all \
    && rm -rf /var/cache/yum/*

ENV JAVA_HOME /etc/alternatives/java_sdk_1.7.0
ENV ANT_HOME /usr/local/ant
ENV CLASSPATH $CLASSPATH:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar:${ANT_HOME}/lib
ENV PATH $PATH:$JAVA_HOME/bin:$ANT_HOME/bin
