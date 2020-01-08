############################################################
# Dockerfile to build centos 6.7 + java 
# Based on centos 6.7
# install java 8 to /usr/local/java
# Change yum sources to https://mirrors.tuna.tsinghua.edu.cn/
# How to build new image: docker build -t  yoho-java
############################################################

#base image cento 6.7
FROM centos:6.7
 
MAINTAINER  chunhua.zhang  <chunhua.zhang@yoho.cn>

label container yoho-java


# Prepare environment 
ENV TZ "Asia/Shanghai"
ENV JAVA_HOME /usr/local/java
ENV PATH $PATH:$JAVA_HOME/bin

# 1.install some useful tools
RUN yum install -y telnet \
    yum install -y tar \
    yum install -y wget

# 2.modify centos 6 repo to tsinghua: https://mirrors.tuna.tsinghua.edu.cn/
RUN wget https://raw.githubusercontent.com/YOHO-LAB/dockerfiles/master/yoho-java/tsinghua-centos6.repo
RUN mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
RUN cp tsinghua-centos6.repo /etc/yum.repos.d/CentOS-Base.repo
RUN  yum makecache

# 3.install java 8 
ENV JAVA_VERSION 8u131
RUN wget   http://blob.yohops.com/software/jdk-${JAVA_VERSION}-linux-x64.tar.gz && \
 tar -xvf jdk-${JAVA_VERSION}-linux-x64.tar.gz && \
 rm jdk*.tar.gz && \
 mv jdk* ${JAVA_HOME}
