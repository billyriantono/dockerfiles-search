#Dockerfile centos-with-java
# 选择一个已有的os镜像作为基础
FROM wuyl/centos-with-ssh:latest

# 镜像的作者
MAINTAINER wuyl

# 安装wget
RUN yum install -y wget

# 下载jdk8并安装
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.rpm
RUN rpm -ivh jdk-8u181-linux-x64.rpm

# 安装epel仓库
RUN yum install -y epel-release
