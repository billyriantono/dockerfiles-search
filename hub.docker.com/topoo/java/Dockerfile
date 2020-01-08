FROM centos:7.6.1810

MAINTAINER topooo

RUN yum update -y && \
    curl --insecure --junk-session-cookies --location --remote-name --silent --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u202-b08/1961070e4c9b4e26a04e7f5a083f551e/jdk-8u202-linux-x64.rpm && \
    yum localinstall -y jdk-8u202-linux-x64.rpm && \
    rm jdk-8u202-linux-x64.rpm && \
    yum -y install unzip && \
    curl --insecure --location --remote-name --silent http://repo1.maven.org/maven2/com/vip/vjtools/vjtop/1.0.8/vjtop-1.0.8.zip && \
    unzip vjtop-1.0.8.zip -d /opt && \
    rm vjtop-1.0.8.zip && \
    yum clean all

RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone

ENV JAVA_HOME=/usr/java/jdk1.8.0_202-amd64/ \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8